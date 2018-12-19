<html>
<h1>Fetching Transactions</h1>
    
<p>This tutorial explains how to fetch existing transactions using IRI and the Python IOTA client library, called [PYOTA](https://github.com/iotaledger/iota.lib.py).</p>

<h2>Prerequisites</h2>

<p>To replicate the examples use the following:</p>

<ul>
<li>An installation of Python (2.7/3.5/3.6)</li>
<li>PIP (Python package manager)</li>
<li>A virtual environment to run our application in (not required but highly recommended)</li>
<li>The iota.lib.py package (<code>pip install pyota</code>)</li>
</ul>

<p>You can run these examples in a Python script or a interactive Python shell session. </p>

<h2>Connecting to a node</h2>

<p>Before you can start using the client you must import it and initialize it with a node address to connect to:</p>

<pre><code>from iota import Iota

api = Iota(&#39;https://nodes.iota.cafe:443&#39;)
</code></pre>

<p>If you want to be able to fetch transactions as well for a given seed you can provide that as well when initializing the library:</p>

<pre><code>api = Iota(&#39;https://nodes.iota.cafe:443&#39;, &#39;YOURSEEDHERE&#39;)
</code></pre>

<h2>Fetching the total balance using a seed</h2>

<p>In order to fetch transactions first make a selection of what transactions you want to look for. A common use case would be to fetch transactions by providing a single address, or all addresses belonging to a certain seed. If you&#39;ve initialized your library with a seed you can simply run the get_inputs method to fetch all addresses with transactions belonging to your seed:</p>

<pre><code>addresses = api.get_inputs()
</code></pre>

<p>This will return the addresses it can find for the given seed with transactions and the total balance:</p>

<pre><code>{&#39;inputs&#39;: [Address(b&#39;IBTLTWJPCA9BKUIHAUDDKM9ZLKYBDJNTNJESCNBK9IBBQPDJKRXSPIQYHXNRMEBILGFPKXNUOFXMHHENX&#39;)],
 &#39;totalBalance&#39;: 1}
</code></pre>

<p>In this example the total balance is 1 iota and there&#39;s only 1 address used for this seed.</p>

<h2>Fetching balances using a list of addresses</h2>

<p>If you wish to fetch the confirmed balance for a single address or multiple addresses without having to provide the seed to your code you can do so as well:</p>

<pre><code>api.get_balances(addresses=[&#39;IBTLTWJPCA9BKUIHAUDDKM9ZLKYBDJNTNJESCNBK9IBBQPDJKRXSPIQYHXNRMEBILGFPKXNUOFXMHHENX&#39;])
</code></pre>

<p>This will return:</p>

<pre><code>{&#39;balances&#39;: [1],
 &#39;milestone&#39;: None,
 &#39;duration&#39;: 0,
 &#39;milestoneIndex&#39;: 915595,
 &#39;references&#39;: [&#39;ZKYQEHDDFWTTZUFTXWYYFZOPVNDMECNVXDBPNMDZAQQJLE9HAAQVZWWPEGSFSUWMMYBBCCIZDAKKA9999&#39;]}
</code></pre>

<p>If you just need an overview of confirmed balance for certain addresses this might be all you need for your use-case.</p>

<h2>Finding transactions</h2>

<p>To find the actual transaction hashes for a certain address, or a lost of addresses, use the <code>find_transaction</code> method:</p>

<pre><code>hashes = api.find_transactions(addresses=[&#39;IBTLTWJPCA9BKUIHAUDDKM9ZLKYBDJNTNJESCNBK9IBBQPDJKRXSPIQYHXNRMEBILGFPKXNUOFXMHHENX&#39;])  
</code></pre>

<p>This returns a dictionary with a list of hashes and the duration it took to process the request:</p>

<pre><code>{&#39;hashes&#39;: [TransactionHash(b&#39;IADZ9GCZY9CJJKGQMTQBPWJUYKOPPDVOGAFNAIOEJ9YA9TAJCZKQREECMFGXEUFUMZPEBFFGLEVWZ9999&#39;),
TransactionHash(b&#39;PLURFNVBVAOOZFOLDGGGBOONTJIES99YXSVYGGQ9WBAIOM9WFRSZXBRQWKZKRQAZTFVYQKLDSGQF99999&#39;),
TransactionHash(b&#39;THPIWTNWST9ALTNIMNHIGCIHAIZCRHNCARFRDIUHKRPASBNE9PC9MVWXXAINJFIREWZAFGFVENGPA9999&#39;),
TransactionHash(b&#39;D99NDB9FFWSNOEKNVNOWJPZIXVGCVKHNNJAVMMFSXXGALGANIUJJRKDNVTY9OXFXKQCUAFGOYMPWA9999&#39;)],
 &#39;duration&#39;: 0}
</code></pre>

<p>These hashes by itself are not very useful to us, but they can be used in the next step to fetch the bundle(s) associated with them for more details.</p>

<h2>Checking if transactions are confirmed</h2>

<p>The transaction hashes returned by the <code>find_transactions</code> method can be both confirmed or unconfirmed. If you need to be sure the transactions you are handling are confirmed you should check the inclusion state of your transactions. The inclusion state of the transaction tells you if the transaction is confirmed by a milestone. For financial transactions you should always check this.</p>

<pre><code>included = api.get_latest_inclusion(hashes[&#39;hashes&#39;])
</code></pre>

<p>This returns a dictionary with a single &#39;states&#39; key, this entry contains another dictionary with as the key the Transaction Hash and as the value either True or False (included or not). If you only want the TransactionHashes that are actually confirmed, then loop over them and check if they have a <code>True</code> value:</p>

<pre><code>confirmed_hashes = []

for txhash, confirmed in included[&#39;states&#39;].items():
    if confirmed:  
        confirmed_hashes.append(txhash)
</code></pre>

<p>Our <code>confirmed_hashes</code> list now only contains the transactions hashes that are actually referenced by a milestone:</p>

<pre><code>[TransactionHash(b&#39;XMPMUTUONRQIDYBDQDZLMKIIWJTWYLATSNJOGHFIYJNPUOLNTZVWVFJBLUVR9TEGKHODBUZYDVFO99999&#39;),
 TransactionHash(b&#39;THPIWTNWST9ALTNIMNHIGCIHAIZCRHNCARFRDIUHKRPASBNE9PC9MVWXXAINJFIREWZAFGFVENGPA9999&#39;), 
 TransactionHash(b&#39;D99NDB9FFWSNOEKNVNOWJPZIXVGCVKHNNJAVMMFSXXGALGANIUJJRKDNVTY9OXFXKQCUAFGOYMPWA9999&#39;)]
</code></pre>

<h2>Fetching a bundle and transactions by a transaction hash</h2>

<p>To fetch the bundle(s) for a transaction hash call the <code>get_bundles</code> method:</p>

<pre><code>bundles = api.get_bundles(&#39;IADZ9GCZY9CJJKGQMTQBPWJUYKOPPDVOGAFNAIOEJ9YA9TAJCZKQREECMFGXEUFUMZPEBFFGLEVWZ9999&#39;)
</code></pre>

<p>This returns a dictionary with a bundles key containing a list of Bundle objects, often times this will just be a single bundle. A bundle object has a <code>transactions</code> attribute.  Loop over all transactions within our bundle for details:</p>

<pre><code>for bundle in bundles[&#39;bundles&#39;]:
    for transaction in bundle.transactions:
        print(transaction)
</code></pre>

<p>This will print something like this for every transaction within the bundle:</p>

<pre><code>Transaction(**{&#39;hash_&#39;: TransactionHash(b&#39;IADZ9GCZY9CJJKGQMTQBPWJUYKOPPDVOGAFNAIOEJ9YA9TAJCZKQREECMFGXEUFUMZPEBFFGLEVWZ9999&#39;),
             &#39;signature_message_fragment&#39;: Fragment(b&#39;CCTCGDHD9999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999&#39;),
             &#39;address&#39;: Address(b&#39;IBTLTWJPCA9BKUIHAUDDKM9ZLKYBDJNTNJESCNBK9IBBQPDJKRXSPIQYHXNRMEBILGFPKXNUOFXMHHENX&#39;),
             &#39;value&#39;: 1,
             &#39;legacy_tag&#39;: Tag(b&#39;HRINITY99999999999999999999&#39;),
             &#39;timestamp&#39;: 1544107591,
             &#39;current_index&#39;: 0,
             &#39;last_index&#39;: 3,
             &#39;bundle_hash&#39;: BundleHash(b&#39;E9ZSGZYXBGWL99QUKBQKIPLKGVROU9CXXGHXVLOSTGZOWHDINJKFIYX9ECDWHBLDQ99AHTGUVUBQPRGZ9&#39;),
             &#39;trunk_transaction_hash&#39;: TransactionHash(b&#39;INZZO9QDEGUBLKLCKOYCVSSYZIMQZWZKJ9OIFZXSFCLIUAEKCVQXM9CYDEURECGOLOMREOAJDINHZ9999&#39;),
             &#39;branch_transaction_hash&#39;: TransactionHash(b&#39;OASP9EMDBEOFBARVYFVRTHK9XRIGYBHSVIBRITAFGOQRSNBKZAXRGPMRCAFCZVXJ9Z9PCZ9XMIYQ99999&#39;),
             &#39;tag&#39;: Tag(b&#39;TRINITY99999999999999999999&#39;),
             &#39;attachment_timestamp&#39;: 1544107600248,
             &#39;attachment_timestamp_lower_bound&#39;: 0,
             &#39;attachment_timestamp_upper_bound&#39;: 3812798742493,
             &#39;nonce&#39;: Nonce(b&#39;ESARJ9999999999999999999999&#39;)})
</code></pre>

<p>This transaction object contains all available data about a transaction including the value, address it refers to, a tag and a signature or message fragment. You can use this data as you please for your use-case.</p>

<p>Our bundle object also comes with a handy <code>get_messages</code> function that will extract all encoded messages within the bundle (for example the messages you enter when you send a transaction through Trinity).</p>

<pre><code>bundle.get_messages()
</code></pre>

<p>Returns:</p>

<pre><code>[&#39;Test&#39;]
</code></pre>

<h2>A shortcut to fetch all transactions for a given seed</h2>

<p>If you just want to fetch a complete history (as known by the node you are connected to) of all transfers connected to your seed there is a handy shortcut available in the form of the <code>get_transfers</code> function. This function will fetch all bundles for all addresses for the seed. Optionally you can ask the function to check for the inclusion state as well so you can check if the bundles are confirmed. After they are returned by the function:</p>

<pre><code>bundles = api.get_transfers(inclusion_states=True)
</code></pre>

<p>This function returns the same dictionary as the <code>get_bundles</code> function above containing all the bundles for all our addresses with transactions. Since we asked for the inclusion state as well you can easily check each bundle to see if it is confirmed:</p>

<pre><code>for bundle in bundles[&#39;bundles&#39;]:
    if bundle.is_confirmed:
        print(&#39;bundle %s is confirmed&#39; % bundle.hash)
        # You can add your code to process this confirmed bundle here!
</code></pre>

<p>It&#39;s tempting to use this method because it&#39;s quick and easy to implement but there is a big caveat; It can become incredibly slow if you have a lot of transactions or addresses with transactions for your seed. For faster processing it is highly recommended to keep a state of what you already processed before so you don&#39;t have to fetch every transaction every time you want to see if there&#39;s a change. A example of keeping state is storing your total confirmed balance and already processed transaction hashes in a database and only check a new transaction if it&#39;s not in the processed database yet. This can make a huge difference in execution time for your application.</p>

<h2>Full example: showing all confirmed value transactions for a seed, including messages</h2>

<pre><code>from iota import Iota

# Connect to our node with our seed
api = Iota(&#39;https://nodes.iota.cafe:443&#39;, &#39;YOURSEEDHERE&#39;)

# Get all addresses for our seed with actual transactions, including balance
inputs = api.get_inputs()
print(&#39;Total balance: %s iota&#39; % inputs[&#39;totalBalance&#39;])
addresses = inputs[&#39;inputs&#39;]

# Find all transaction for our addresses
transactions = api.find_transactions(addresses=addresses)
hashes = transactions[&#39;hashes&#39;]

# Check if our transactions have been confirmed by a milestone
checked_hashes = api.get_latest_inclusion(hashes)

for hash, included in checked_hashes[&#39;states&#39;].items():
    if not included:  
        # The transaction is not confirmed, let&#39;s skip this one!
        continue

    bundles = api.get_bundles(hash)

    for bundle in bundles[&#39;bundles&#39;]:
        for transaction in bundle.transactions:

            # Skip transactions without value or negative value
            if transaction.value &lt;= 0:
                continue

            # Skip transactions that are not referencing one of our addresses
            if not transaction.address in addresses:
                continue

            # All remaining transactions should be incoming value transactions

            message = transaction.signature_message_fragment.as_string()

            print(&#39;Received: %s iota with message: %s&#39; % (transaction.value, message))
</code></pre>

<p>If this seed has any confirmed incoming transactions you should see a output similar to this:</p>

<pre><code>Total balance: 7 iota
Received: 6 iota with message: Hello
Received: 1 iota with message: Test
</code></pre>
</body></html>

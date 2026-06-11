# SimpleHash

This utility is designed to let you quickly and easily hash some text. It defaults to sha256 - less config means less fiddling to match hashes with another person.

### Expected use

Considering how good deepfakes can get, this site is intended to help people verify that they are texting with who they think.

First, you should come up with one-time passwords for the person you intend to communicate with, and share them in-person.

Then, to verify you're speaking to who you think, and send an un-fakeable message, open this site and find the hash of something like this:

"password1:This is bob"
asdfasdfasdfasdf

Send the person two messages, NEITHER of which has password1:
"This is bob"
"Hash was asdfasdfasdf" 

If the recepient also knows password1, they can also go to this site and put in exactly

"password1:This is bob" 

and see the same hash out, asdfasdfasdf. If a hacker or government doesn't know password1, it will take more computing power than in the entire world to go from asdfasdfasdf back to password1, even if they know the message "This is bob". If a hacker tries to say "this is bob" "hash was aaaaaaaaaaaaa", giving some fake hash, then your recepient won't get a match with asdfasdfasdf and will know that the sender doesn't know password1. 

### Verifying the site
It would be easy for this website to be hacked, and for someone to steal the plaintext "password1:This is bob". 

To prevent this, this site is dirt simiple. Anyone should be able to look at the HTML, which is the raw code on your computer, and instantly verify there's nothing fishy going on. 

If you open the website details ("inspect" in chrome), the element tree should look like what it says below, identical to the contents of index.html page. The most important thing is that there is only one `<script> </script>`, and its contents should be identical to what you see below; but if you see any discrepancies you don't understand, you should assume the site is not secure and don't put password1 into it.

```
<body>
  <h4><a href="placeholder">Instructions</a></h4>
  <input id="i" placeholder="Type...">
  <p id="o">0000</p>

  <script>
    i.oninput = async () => {
      const buf = await crypto.subtle.digest('SHA-256', new TextEncoder().encode(i.value));
      o.textContent = btoa(String.fromCharCode(...new Uint8Array(buf)));;
    };
  </script>
</body>
```


### Development

Just open the index.html file in your browser :P 


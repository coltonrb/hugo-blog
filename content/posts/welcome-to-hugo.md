---
title: "Welcome to Axiomatic Caribou's blog"
date: 2019-06-01T00:55:23Z
draft: false
---


Devyn talked me into doing a coding challenge to start a website. I decided to build it in AWS on Hugo 

0:00 START

7:08 AWS server provisioned and accessed via SSH. AWS firewall enabled and restricted to 22, 80, and 443/tcp

10:46 Realized I didn't really want the AWS Linux AMI (appears incompatible with Snap, which I wanted to try), so re-created VPS with Debian.

15:32 Re-created and bback running.

16:52 Hugo installed via snap

20:56 Site created and template first post created

22:33 SSH reverse tunnel set up on port 1313 to be able to view Hugo development server

23:28 tmux installed so I can edit an article while keeping a dev server open in a different terminal

31:56 Docker installed and configured to run as non-root user as per [here](https://docs.docker.com/install/linux/linux-postinstall/). I'm now following [these instructions](https://medium.com/@pentacent/nginx-and-lets-encrypt-with-docker-in-less-than-5-minutes-b4b8a60d3a71) to get the site served up with nginx and Let's Encrypt.

I realized I've got a bit of a snag: I want to serve my site exclusively over TLS, but I don't have a domain name for it, and Let's Encrypt will only issue certs for domains, not IPs. I wonder if I can get a cert issued for the AWS DNS domain name...

35:20 Docker Compose up and running

43:26 `Error creating new order :: Policy forbids issuing for name` Well, worth a shot. Hmmm... 

44:24 I'm going to take a break for a bit to think on this. I'll pause time and come back in a bit.

46:00 Decided to just map `coltonrb.com` onto the IP.

48:30 Looks like I've got Dynamic DNS set up for `coltonrb.com` right now? I didn't think I did...

51:03 Set up an A record for `hugo.coltonrb.com` to point to the server

59:56 UFW installed and configured

71:17 I failed a few times to get LetsEncrypt up and running, and hit ratelimiting. Alas. Well, as per LetsEncrypt, "There is a Failed Validation limit of 5 failures per account, per hostname, per hour. This limit is higher on our staging environment, so you can use that environment to debug connectivity problems." Welp. See you in an hour.

127:45 Finally waited out the timeout and sorted out the barriers to the certificate. I had to drop the TLS config from nginx so it only served the challenge over HTTP - something in the script wasn't creating the dummy certificates correctly. I also discovered a switch in the script that let me hit Let's Encrypt's staging environment without ratelimiting.

145:23 Found the typo that so eluded me. The nginx config referred to an incorrect path for the key's `fullchain.pem` file. Everything's working great now, just need to point it at the Hugo directory...

148:50 Hugo site built

150:27 IT WORKED I can access the blog

152ish: Copied this post into a post and completed the challenge.




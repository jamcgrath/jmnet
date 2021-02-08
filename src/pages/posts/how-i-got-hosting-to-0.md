---
title: How I got my hosting costs to $0
date: "2021-02-08"
template: post
excerpt: Using GCP, Github Pages and Netlify I reduced my hosting costs by 96%
---

<em>This post is not a tutorial but just an account of what I did. For each website that was moved to a new webhost there is a high level list of things that were done. </em>

## THE IDEA
During my break for new years, I decided that I would attempt to reduce my web hosting costs to $0/¥0. At the time I was spending about $10 a month using WebFaction. The reasons I decided to this were:
- My personal sites use Netlify and Firebase hosting.
- The four sites on WebFaction are either WordPress or static and they are low traffic websites.
-  These days there are so many options for free/ cheap cloud hosting that it didn't seem to make sense paying $120 a year.
-  WebFaction was bought by GoDaddy about year or so ago.

## HOSTING REQUIREMENTS
My hosting requirements are very simple. I needed to host two static HTML websites and two WordPress instances.

## HOSTING OPTIONS
These days there are many free or cheap cloud hosting options. I took some time to look at all the options I thought might fit my needs. These were cloud services like AWS and GCP, VPS services like Linode, Vultr and Digital Ocean and straight up  cheap webhosting like Bluehost and the like.

I decided to go with Netlify, GitHub pages and GCP.  These are the reasons for those choices.
- I'm familiar with using Netlify and GitHub pages.
- Netlify has an easy mail form setup. I didn't want to have to integrate a third party mail service like Wufoo or Formspree.
- I'm studying to take the GCP Associate Cloud Engineer Exam. Using this would give me some real world experience.

Netlify and GitHub pages will work for the static sites I need to host and GCP will get the WordPress instances.

## ACTUALLY CHANGING HOSTING
The first 2 sites I decided to move were my friends moped shop websites. These sites were already static or at least I thought they were. Turns out one of the had some quick and dirty php for mail form.

### Moped Site A
I chose GitHub pages for this site because it doesn't have a mail form.
The steps to move were:
1. Download the website via ftp
2. Init git in the directory I downloaded it, then commit and push to github/
3. Enable pages on GitHub and assign a custom domain to the page by setting an A record at the domain registrar to point to the GitHub pages IP address.
4. Setup the mx records for their Google Workspace

### Moped Site B
This site had the quick and dirty PHP code for the mail form. The initial plan was to use GitHub pages for this site too. Since it had a mail form I decided to use Netlify instead.
The steps to move this site were:
1. Download the website and init git and commit and push.
2. Remove the php and replace and add the Netlify mail form attributes to the mail form.
3. Deploy with Netlify
4. Assign their domain and setup Google Workspace MX records on Netlify.

## My Partner's website.
After looking at my partners website, I had a discussion with them about converting their website to a static HTML site because they don't use any WordPress features. To do the conversion I used HTTRACK. Which initially failed. I think the reason was that there is some weird redirect shenanigans going on with WebFaction to get SSL to work.

The Steps for moving this were:
1. Clone the website with Duplicator and install locally.
2. Run HTTRACK on the local install to get the html pages.
3. Go through the code and remove some unnecessary HTML that is created by WordPress, plugins or the theme.
4. Replace the form with Netlify form and get the Google Maps embed to work.
5. Init git on the cleaned HTML site, commit and push to GitHub
6. Deploy to Netlify.
7. Assign domain and MX records for Google Suite.

## Dixon's website.
This website had to stay a WordPress site. The reason was that it is an custom themed ecommerce website. I didn't want to rebuild this site and I know Dixon definitely doesn't want to pay my rates to do that. The hosting choice for this site was a GCP Micro F1 instance on compute engine.

The steps to do this were:
1. Setup a GCP VM on compute engine using the click to deploy  Wordpress solution from the GCP Marketplace.
2. Download a copy of the site with duplicator.
3. SSH into the vm and delete all the files in the wordpress directory.
4. Copy the duplicator backup files and installer to the wordpress directory on the VM
5. Run the Duplicator installer. Which worked with out an issue installing. However because the site forced ssl on admin login I couldn't login until I edited that line in wp-config.
6. Setup Cloud DNS to handle the domain name
7. Setup SSL using Certbot.

For SSL setup on Dixon's site, I had 2 options. Have GCP manage it or do it myself. I chose to do it myself using Certbot. I thoght I would be a tedious task because I have setup free SSL certificates in the past, but the Certbot script was simple and well documented and I didn't have to calculate when to run a Cron job to renew. The reason I chose to not let GCP manage the SSL is because from my understanding it looks like I would have to setup a load balancer and that seemed kind of overkill.

Getting my hosting cost down to almost $0 was not really that difficult for me. The hardest part was putting WordPress on GCP. That was because I was not too confident in my GCP skills. Like I said earlier, it gave me some real world experience for GCP. However it turns out that I was unable to get to $0. I ended up paying ¥40 a month to Google for using Cloud DNS. $10 to ¥40 is a great reduction.

Overall I would recommend any of these services if you are looking for free hosting and you site is not too complex and not resource heavy.

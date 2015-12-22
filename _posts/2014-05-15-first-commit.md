---
layout: post
title: First Commit
description: "Its ON, baby"
headline: "Let's Fire up the Engines"
categories: 
  - personal
tags: "blogging,jekyll"
imagefeature: "website-speed.jpg"
imagecredit: spreadeffect.com
imagecreditlink: "http://www.spreadeffect.com/blog/improve-website-speed/"
comments: false
mathjax: false
featured: true
published: true
modified: ""
---


    sp<ResourceTable::Package> ResourceTable::getPackage(const String16& package)
    {
      sp<Package> p = mPackages.valueFor(package);
      if (p == NULL) {
        if (mIsAppPackage) {
          if (mHaveAppPackage) {
            fprintf(stderr, "Adding multiple application package resources; only one is allowed.\n"
            "Use -x to create extended resources.\n");
            return NULL;
          }
          mHaveAppPackage = true;
          p = new Package(package, 127);
        } else {
          p = new Package(package, mNextPackageId);
        }
        //printf("*** NEW PACKAGE: \"%s\" id=%d\n",
        //       String8(package).string(), p->getAssignedId());
        mPackages.add(package, p);
        mOrderedPackages.add(p);
        mNextPackageId++;
      }
      return p;
    }
  
But the game was changed when my site got hacked. Wordpress is notorious in getting hacked. The PHP code libraries are huge, and while Automattic tries to keep it relatively clean and bug free, bugs do persist among the thousands of lines of codes and every once in a while a bug gets discovered by the code breakers. If the bug can be exploited in some way to gain access of the site, the code breakers tend to do some serious damage. While I wasn’t been exclusively targeted by such individuals, I was part of a victimized group who used the same version of Wordpress, and all of our sites got defaced by some mass defacing software. Although it didn’t do serious damage, as I have daily off-site backup, I became dubious about the Wordpress platform.


So, this time around, while I was still brainstorming for ideas and theme designs and what not, I decided to go back to Jekyll, or you may say, rather old school. Why not use plain static HTML files with some CSS styling and JS animations? Static sites are impossible to hack, as there are no codes needed to be run on the server. The only way a static site can be compromised if the code breakers have access to your FTP account. I have used Jekyll in the past during my college years. I was working as a Teaching Assistant in the Mathematics Dept, and I was supposed to post weekly course materials on the course website. The trouble was my Alma maters IT dept didn’t allow dynamic sites to run on the nodes, and I wasn’t going download the HTML files, edit them with Sublime text, and push them back onto the server every week. So I used Jekyll and GIT Version Control to do that for me. And it was so efficient that I would post materials daily instead of weekly. It was like love on first use. But Wordpress had lots of theme choices and for my personal site I decided to use Wordpress anyways disregarding the simpleness and speed static sites provided. After the takeover of my Wordpress powered blog happened, I turned to self written PHP sites and static sites completely. I have built a social network based on PHP for my peer group which is highly secure but when it comes down to speed it lags behind. So I built this site using Jekyll, a blog aware static site generator. I hope this site will perform as envisioned.

[^1]: This domain previously hosted a Wordpress blog.

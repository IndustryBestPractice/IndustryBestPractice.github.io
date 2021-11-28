---
layout: post
title:  "K.I.S.S. - Questions to ask when setting up a new project or service"
date:   2021-11-27 05:00:01 -0500
categories: ['projects', 'checklist']
author: '@_mbanana'
---

<div class="post-categories">
  {% if post %}
    {% assign categories = post.categories %}
  {% else %}
    {% assign categories = page.categories %}
  {% endif %}
  Categories: {% for category in categories %}
  <a href="{{site.baseurl}}/categories/#{{category|slugize}}">{{category}}</a>
  {% unless forloop.last %}&nbsp;{% endunless %}
  {% endfor %}
</div>
<br>
Standing up new services or products isn't always easy, but asking the right questions aught to be. There are much more detailed questions that need to be asked but breaking concepts into critical domians of interest have helped the non-technical teams to ask the easy questions first without involving the information security department in every initial meeting and discussion.

### DATA
* What data are you sending?
* Do you need to send all that data or are only a few fields or items required?
* Is any of it sensitive?
* Is any of it compliance enforced (PCI, SOX, HIPAA, etc)?

### TRANSFER
* How are you getting the data from A -> B?
	* (S)FTP
	* API
	* Other
* Are you sending data to them, or are they reaching in and grabbing it from you?
* How are you securing this communication?
	* Certificate?
	* Point-to-Point VPN?
	* Other

### AUTHENTICATION
* Is the product/service SSO integrated?
* Does it integrate with YOUR SSO solution (Azure AD, ADFS, SAML, OKTA, whatever)
* How are you going to handle "break the glass" accounts that cannot be federated?
* Is it MFA or 2FA?

### AUTHORIZATION
* Does it support Role Based Access Control (aka RBAC)?
* How will those roles be provisioned automatically (AD synced groups, etc) or manually assigned by an administrator?

### EXTERNAL PARTY ACCESS
* Who else, outside of your core employees, needs access to this information (vendors, trusted partners, marketing, etc)

### SYSTEM ATTACK SURFACE
* Is this required to be on the internet (i.e. accessible from the world)
* Are there any NAT or Port Forwarding requirements
* Is there additional infrastructure that is required for this solution? (i.e. a WAF, DMZ proxy server, etc)
* Does this require a subscription to any cloud service (AWS, GCP, Azure)
* Will access to this service be from inside your own network or accessed from anywhere in the world?
* Does it have IP allow listing?

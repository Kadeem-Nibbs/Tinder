# Tinder API Documentation -- 2017

First off, I want to give a shoutout to <a href='https://gist.github.com/rtt/10403467#file-tinder-api-documentation-md'>@rtt</a> who initially posted the Tinder API Documentation that I found most of these endpoints on. I am writing this to provide a more up-to-date resource for working with the Tinder API.

**Note: This was written in February 2017. API might be outdated.**

### API Details 
<table>
	<tbody>
		<tr>
			<td>Host</td>
			<td>api.gotinder.com</td>
		</tr>
		<tr>
			<td>Protocol</td>
			<td>SSL</td>
		</tr>
	</tbody>
</table>

### Required Headers
<table>
	<thead>
		<tr>
			<th>Header</th>
			<th>Example</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>X-Auth-Token</td>
			<td>See "How to get facebook_token" below</td>
		</tr>
		<tr>
			<td>Content-type</td>
			<td>application/json</td>
		</tr>
		<tr>
			<td>User-agent</td>
			<td>Tinder/4.7.1 (iPhone; iOS 9.2; Scale/2.00)</td>
		</tr>
	</tbody>
</table>

### Known Endpoints
Note: All endpoints are concatenated to the host api

Note: All curls must be sent with the headers as well (the only exception is that the /auth call must not have the X-Auth-Token header)
<table>
	<thead>
		<tr>
			<th>Endpoint</th>
			<th>Purpose</th>
			<th>Data?</th>
			<th>Get/Post/Delete</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>/auth</td>
			<td>For authenticating</td>
			<td>{'facebook_token': INSERT_HERE, 'facebook_id': INSERT_HERE}</td>
			<td>POST</td>
		</tr>
		<tr>
			<td>/user/recs</td>
			<td>Get match recommendations</td>
			<td>{}</td>
			<td>GET</td>
		</tr>
		<tr>
			<td>/user/matches/_id</td>
			<td>Send Message to that id</td>
			<td>{"message": TEXT GOES HERE}</td>
			<td>GET</td>
		</tr>
		<tr>
			<td>/user/_id</td>
			<td>Get a user's profile data</td>
			<td>{}</td>
			<td>GET</td>
		</tr>
		<tr>
			<td>/user/ping</td>
			<td>Change your location</td>
			<td>{"lat": lat, "lon": lon}</td>
			<td>POST</td>
		</tr>
		<tr>
			<td>/updates</td>
			<td>Get all updates since the given date -- inserting "" will give you all updates since creating a Tinder account (i.e. matches, messages sent, etc.)</td>
			<td>{"last_activity_date": ""}</td>
			<td>POST</td>
		</tr>
		<tr>
			<td>/profile</td>
			<td>Get your own profile data</td>
			<td>{}</td>
			<td>GET</td>
		</tr>
		<tr>
			<td>/profile</td>
			<td>Change your search preferences</td>
			<td>{"age_filter_min": age_filter_min,
				"gender_filter": gender_filter,
				"gender": gender,
				"age_filter_max": age_filter_max, 
				"distance_filter": distance_filter}</td>
			<td>POST</td>
		</tr>
		<tr>
			<td>/meta</td>
			<td>Get your own meta data (swipes left, people seen, etc..)</td>
			<td>{}</td>
			<td>GET</td>
		</tr>
		<tr>
			<td>/report/_id</td>
			<td>Report someone --> There are only a few accepted causes...</td>
			<td>{"cause": CAUSE}</td>
			<td>POST</td>
		</tr>
		<tr>
			<td>/like/_id</td>
			<td>Like someone a.k.a swipe right</td>
			<td>{}</td>
			<td>GET</td>
		</tr>
		<tr>
			<td>/pass/_id</td>
			<td>Pass on someone a.k.a swipe left</td>
			<td>{}</td>
			<td>GET</td>
		</tr>
		<tr>
			<td>/like/_id/super</td>
			<td>~Super Like~ someone a.k.a swipe up</td>
			<td>{}</td>
			<td>GET</td>
		</tr>
		<tr>
			<td>/group/{like|pass}/_id</td>
			<td>Like or Pass on a group</td>
			<td>{}</td>
			<td>GET</td>
		</tr>
	</tbody>
</table>

### Status Codes
<table>
	<thead>
		<tr>
			<th>Status Code</th>
			<th>Explanation</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>200</td>
			<td></td>
		</tr>
		<tr>
			<td>400</td>
			<td></td>
		</tr>
		<tr>
			<td>501</td>
			<td></td>
		</tr>
	</tbody>
</table>

### Dependencies:
<ul>
	<li> datetime </li>
	<li> threading </li>
	<li> requests </li>
	<li> json </li>
	<li> re </li>
	<li> robobrowser </li> 
</ul>

### Config File
<h3> <strong> facebook_access_token and fb_user_id </strong></h3>

Very simple now. Just input your facebook username/email and password in your config file. Then, the fb_auth_token.py module will programmatically retrieve your facebook_access_token and fb_user_id. These are then used to generate your tinder_auth_token in tinder_api.py! Happy Swiping!
<br>

<strong> ** </strong> To see the non-programmatic way to get your facebook_access_token and facebook_id, visit <a href=https://github.com/fbessez/Tinder/blob/master/AuthPhotos/README.md> this README </a> and follow the instructions! <strong> ** </strong> 

<strong> Note: </strong> With the help of <a href=https://github.com/philipperemy/Deep-Learning-Tinder/blob/master/tinder_token.py> philliperemy </a>, I have included a programatic way to acquire your facebook_token. Now, in your config.py just input your facebook username and password as paramaters to the get_fb_access_token function.

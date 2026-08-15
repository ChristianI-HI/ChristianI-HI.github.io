---
layout: project
type: project
image: "img/musiciansofmanoa/logo.png"
title: "Musicians of Manoa"
date: 2024
published: true
labels:
  - React
  - Next.js
  - PostgreSQL
  - Prisma
  - Agile Project Management
summary: "A full-stack Next.js app helping UH Mānoa students find musicians and jam sessions matching their skills."
featured: true
---

<div class="text-center p-4">
  <img src="../img/musiciansofmanoa/home.png" class="img-thumbnail" >
</div>

<hr>

## Introduction
<p>
This group project was the final project in my ICS 314 class at the University of Hawaii at Manoa. My group consisted of four people all with varying levels of programming experiences as well as tech stack preferences ranging from creative design to database programming. However, being the cumulative project of all the skills and experiences we developed alongside each other as a class, we were able to work as a cohesive programming team and pump out a functioning web app with features that built atop the baseline ICS 314 set for us. This project highlights profiency using frameworks such as NextJs, designing relational databases with PostgreSQL, and soft-skills related to project management such as communication and accountability.
</p>
<br>

## Features
<p>
The purpose of the Musicians of Manoa web app is to connect the musical talents of UH Manoa, inviting students, faculty, or alumni a common platform to highlight their musical abilities and connect through musical jam sessions that align with their tastes and experience. The actual web app features users to personalize their profile by musical tastes, experience level, goals, and instruments which is then uploaded to the application database to be shared to all users who access the website. Users can also create and view musical jam sessions, musical events ranging from classical orchestra to dance parties to casual improvisation on the beach. There were goals to allow users to directly interact with one another, but we only got as far as implementing attendee lists for each musical jam session.
</p>
<div style="display: flex; justify-content: space-between;">
  <img src="../img/musiciansofmanoa/jam.png" alt="Musical Jams featured on Musicians of Manoa" style="width: 45%;">
  <img src="../img/musiciansofmanoa/profile.png" alt="User Profiles featured on Musicians of Manoa" style="width: 45%;">
</div>
<p>
On the moderation side, Admins are able to access, edit, and remove all of the types of content currently available on the website. This includes user-editable data related with musical jam sessions and user profiles and admin-specific data such as profile customization options for user profiles. All relevant components of the website were properly connected to the application database alongside permission handlers, allowing users to write to select parts of the database such creating or editing their own profile or a jam session, but not profiles or sessions created by other users. And of course, users are able to read from the database during the previous description of the website functionality. 
</p>
<br>

## Contribution
<p>
I built the <b>admin interface</b> for managing user profile options, handled <b>availability testing</b>, and maintained our team's Vercel <b>deployment pipeline</b>. Also, though not really a role, as I had relatively more experience with software development than my group mates I often helped debug errors ranging from UI to database management. As all the pages I worked on dealt with database management on the admin end, they were very similar in design (one of the pages shown in the image below) so I encountered difficulty in this project when integrating database interactions into this web application. The actual relational database implementation was easy for me as I've previously taken a database management class, so once I was able to figure out how to update the database from one page, I could easily do same for the rest.
</p>

<div class="text-center p-4">
  <img src="../img/musiciansofmanoa/admingenre.png" class="img-thumbnail" >
</div>

<p>
This project made use of prisma libraries to implement a method for communication between the user/server on the webpage and the database hosted separately. The difficulty of my contribution to the project mainly came from understanding how to weave between the user-server interface and sync variables across that interface. From the server to the database was relatively simple as ICS 314 provides plenty of experience with that. I really wanted to make the admin edit pages able to read and write to the database on the same page, whereas previous in-class designs would redirect to another page. For the longest time I was stumped because on the client-side it looked like the data was being updated, as the text in the table on the site would change, but a simple refresh would revert those changes because the database wasn't actually edited. There as nothing wrong with my database function to push updates to the database, and the client was able to correctly edit the database on the user-end, and it turns out I wasn't actually updating a useState which the server used to connect to the database. From that experience though, I have full confidence in implementing a sleek seamless admin page which edits databases.
</p>

## Links
<ul>
  <li><a href="https://musicians-of-manoa.github.io/"><strong>Homepage</strong></a></li>
  <li><a href="https://musicians-of-manoa.vercel.app/"><strong>Live Deployment</strong></a></li>
  <li><a href="https://github.com/musicians-of-manoa/musicians-of-manoa"><strong>Source Code</strong></a></li>
</ul>
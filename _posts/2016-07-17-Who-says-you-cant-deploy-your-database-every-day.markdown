---
layout: post-index
date: 2016-07-17
img: 
alt: image-alt
tag: [none]
category: [Database, DevOps]
comments: true
---
<iframe src="https://channel9.msdn.com/Events/TechEd/NewZealand/2014/DBI317/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>
In this video from the New Zealand 2014 TechEd conference Hannah Gray demonstrates how to perform database development using SQL Server Data Tools (SSDT) and use continuous integration (CI) with Microsoft Team Foundation Server (TFS) to produce a Data-tier Application Component Package (DACPAC).

### Key takeaways:

1. Using a DACPAC file, which is available as of SQL Server 2012, may streamline the deployment of database changes and simplify the release management process by enabling versioning of database schema. (Similar to how JAR files are used in Java development)
2. A database development workflow using SSDT provides an integrated development experience using one tool which may increase developer productivity. 
3. Automated unit testing, as typically done in software application development, is possible at the database level as well. 
4. The TFS product makes it easy to implement continuous integration at the database level. Similar to how CI is done for application development, a database build can be created in which a commit to source control triggers a build to occur. If successful, the DACPAC output file is produced and saved as part of the build output. 
 
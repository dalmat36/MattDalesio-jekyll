---
layout: post-index
date: 2016-09-08
img: https://s3.amazonaws.com/certificates-mddalesio/ImplementingETLwithSQLServer_edx_09082016-min.PNG
alt: image-alt
tag: []
category: [Professional-Development]
comments: true
---

Earlier this month I finished the Microsoft course: DAT217x: Implementing ETL with SQL Server Integration Services (SSIS) via edX. I found the course very helpful in understanding the fundamentals of SSIS and was able to immediately apply some of the best practices in my current work.  Going into the course I had very little experience with SSIS other than performing a few experiments and afterwards I felt comfortable creating and modifying packages for ETL jobs. I would highly recommend the course if you are already experienced in SQL and SQL Server but are new to SSIS. However, If you have several years of experience already using SSIS you may pick up a few tips on best practices but it might not be what you are looking for.

Key takeaways:

- The primary purpose of SSIS is not to replace SQL but rather provide a visual representation of the ETL process as well as provide some additional capability
- When possible, it is recommend that transformations be performed in Data Flow data sources as opposed to using the SSIS Data Flow Transformations
- Use sequence containers to process data in parallel to reduce execution time
- Avoid transforming large amounts of data directly from a file. Instead import the data to a temporary staging table
- Avoid using SSIS Events to track progress. Instead use logging tables
- Consider removing indexes on the destination tables before loading it
- Avoid implicit conversion. Instead use SQL or C# from outside of the SSIS runtime environment
- Use the SQL Server Destination to improve performance (Uses SQL Server's bulk insert feature)

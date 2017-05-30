# Addendum Builder

Addendum Builder is a custom software tool that makes it easier to build contract-related documents.  Addendum Builder helps you build documents faster, eliminate mistakes, and keep docs organized as well.

The software in this repository is open-sourced under the MIT license, which means you can take it and use it for your own purposes for free.  You can modify it, sell it, or basically do whatever you want with it, as long as you include the licensing information in your work.

As per the license, this software is provided "as is", without warranty of any kind.  If you download the software and use it for your own purposes, you are using it at your own risk.

Here is a link to the (mercifully short) full text of the Addendum Builder MIT license:
  
[https://github.com/addendum1/addendumbuilder/blob/master/LICENSE](https://github.com/addendum1/addendumbuilder/blob/master/LICENSE)

<br/><br/>

---
# Technology

Addendum Builder uses the following technologies:

Component | Technology
--- | ---
Code | C#/.Net, HTML, JavaScript
Database | Microsoft SQL Server (SQL Server 2012 or above recommended)
Encryption | [Crypto-JS](https://code.google.com/archive/p/crypto-js/)
Date Picker Control | [CibulCalendar](https://github.com/kaore/CibulCalendar)
Client-Side File Export | Downloadify Flash Component

<br/><br/>

---
# Installation Guidelines

Guidelines for setting up your own instance of Addendum Builder can be found below.  The basic steps are:
 - Setup the database
 - Clone/copy the code to your local environment
 - Edit the web.config to include your database connection info
 - Deploy the .NET code to the web server

It probably goes without saying, but you'll want to review the code and its associated components to ensure that they meet your organization's security standards.

<br/>

---

### STEP 1: Setup the Database

Create a Microsoft SQL Database for this application by executing a script like this:

```
GO
/****** Object:  Table [dbo].[Docs] ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Docs](
	[Id] [int] NOT NULL,
	[PeepID] [int] NOT NULL,
	[ActiveAsOf] [nvarchar](50) NULL,
	[Status] [nvarchar](50) NULL,
	[DocXML] [nvarchar](max) NOT NULL,
	[MaxVal] [int] NULL,
	[DocType] [nvarchar](50) NULL,
	[CreatedDate] [nvarchar](50) NULL,
	[CreatedBy] [nvarchar](50) NULL,
	[LastUpdatedDate] [nvarchar](50) NULL,
	[LastUpdatedBy] [nvarchar](50) NULL,
	[CnNum] [nvarchar](50) NULL
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[ExportTemplates] ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[ExportTemplates](
	[Id] [int] NOT NULL,
	[Title] [nvarchar](50) NOT NULL,
	[Header] [nvarchar](max) NULL,
	[Footer] [nvarchar](max) NULL
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Peeps] ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Peeps](
	[Id] [int] NOT NULL,
	[PersonEID] [nvarchar](max) NOT NULL,
	[Year] [nvarchar](250) NULL
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[SystemUsers] ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[SystemUsers](
	[Id] [int] NOT NULL,
	[HashedUserID] [nvarchar](500) NOT NULL,
	[HashedUserPW] [nvarchar](500) NOT NULL,
	[Hint] [nvarchar](50) NULL,
	[EditTemplate] [bit] NULL
) ON [PRIMARY]
GO
```
Upon execution, you should have four tables in your database:

Table | Description
--- | ---
Docs | Holds the finished addendum/contract files in text format
ExportTemplates | Stores the base template for output to Microsoft Word
Peeps | Holds the people to which each addendum/contract is associated
SystemUsers | Stores the users of the Addendum Builder system

Note that all data in the database is stored in an encrypted format, and is never unencrypted on the server.  It is transmitted to the browser in an encrypted format, and unencrypted on the end-user's machine using the Crypto-JS package.

<br/>

---
### STEP 2: Clone/Copy the Code

You can find the code in the Github repository, located here:

[https://github.com/addendum1/addendumbuilder](https://github.com/addendum1/addendumbuilder)

Follow standard practices to pull a copy of the code into your environment.

To open and review the code, open the `ContractBuilder1.csproj` file using Visual Studio.

<br/>

---
### Step 3: Edit the Web.config File

You will need to edit the line in the `web.config` file that contains the details of the database connection.

Find this line in the `connectionStrings` section:

> \<add name="connection187" connectionString="Data Source=**DATABASE_SERVER_NAME**;Initial Catalog=**DATABASE_NAME**;Integrated Security=False;User ID=**USERNAME**;Password=**PASSWORD**;Connect Timeout=30;Encrypt=False;TrustServerCertificate=False"/\>

... and replace the placeholders (in bold above) with the appropriate values based on the database that you setup previously in Step 1.

Review the additional `web.config` settings to ensure they are appropriate for your environment.

<br/>

---
### Step 4: Deploy the .NET Code to the Web Server

You'll need to deploy the code to a Microsoft IIS server running .NET 4.0 or above.

In Visual Studio, you'll want to set the Start Action to this specific page: `AddendumBuilder.aspx`.

Build the project in Visual Studio and deploy to the web server.

If you run into build issues, be sure to check that the project's necessary References are all there:

![http://i.imgur.com/cRPhwfq.png](http://i.imgur.com/cRPhwfq.png)

<br/>

---

# Support / Maintenance

No support or maintenance is offered for this repository.  This repository is not actively maintained.



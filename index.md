# Addendum Builder

Addendum Builder is a custom software tool that makes it easier to build contract-related documents.  Addendum Builder helps you build documents faster, eliminate mistakes, and keep docs organized as well.

The software in this repository is open-sourced under the MIT license, which means you can take it and use it for your own purposes for free.  You can modify it, sell it, or basically do whatever you want with it, as long as you include the licensing information in your work.

As per the license, this software is provided "as is", without warranty of any kind.  If you download the software and use it for your own purposes, you are using it at your own risk.

Here is the (mercifully short) full text of the license:

> MIT License
>
>Copyright (c) 2017 AddendumBuilder
>
>Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:
>
>The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
>
>THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

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
# Installation Instructions

Instructions for setting up Addendum Builder can be found below.  The basic steps are:
 - Setup the database
 - Clone/copy the code to your local environment
 - Edit the web.config to include your database connection info
 - Install the .NET code to the web server

It probably goes without saying, but you'll want to review the code and its associated components to ensure that they meet your organization's security standards.

<br/>

---

### STEP 1: Setup the Database

Create a Microsoft SQL Database by executing this script:

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
Docs | Holds finished documents
ExportTemplates | Holds the base template for output to Microsoft Word
Peeps | People to which each document is associated
SystemUsers | Stores the users of the Addendum Builder system

Note that all data in the database is stored in an encrypted format, and is never unencrypted on the server.  It is transmitted to the browser in an encrypted format, and unencrypted there using the Crypto-JS package.

<br/>

---
### STEP 2: Clone/Copy the Code

You can find the code in the Github repository, located here:

LINK!!!!!!!!!!!

Follow standard practices to pull a copy of the code into your environment.

<br/>

---
### Step 3: Edit the Web.config File

You will need to edit the line in the `web.config` file that contains the details of the database connection.


Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/addendum1/addendum1.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.

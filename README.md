# lambda_sample

Prisma Cloud supports AWS Lambda, Google Cloud Functions, and Azure Functions.
Serverless vulnerability and compliance scanning supported by Prisma Cloud
C# (.NET Core) 3.1
Java 8, Java 11
Node.js 12.x, 14.x
Python 3.6, 3.7 and 3.8
Ruby 2.7
Go 1.x

You can scan vulnerabilities using the Jenkins plugin or the  "twistcli" binary  but please  be aware that your  serverless function should be packaged as ZIP file.

* Jenkins pre-reqs
  * Plugins
    * Prisma Cloud plugin

  * Credentials
    * PrismaCloud_creds -- username/password for Twistlock Console with Defender Manager or better role

  * Environment variables
    * Prisma Cloud_CONSOLE -- the FQDN for the Twistlock Console

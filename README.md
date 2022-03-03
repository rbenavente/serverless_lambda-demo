# lambda_sample
Prisma Cloud can scan serverless functions for vulnerabilities. Prisma Cloud supports AWS Lambda, Google Cloud Functions, and Azure Functions.Prisma Cloud can scan Node.js, Python, Java, C#, Ruby, and Go packages.

Scanning functions at build time with twistcli
You can also use the twistcli command line utility to scan your serverless functions. First download your serverless function as a ZIP file, then run:

$ twistcli serverless scan <SERVERLESS_FUNCTION.ZIP>

* Jenkins pre-reqs
  * Plugins
    * Prisma Cloud plugin

  * Credentials
    * PrismaCloud_creds -- username/password for Twistlock Console with Defender Manager or better role

  * Environment variables
    * Prisma Cloud_CONSOLE -- the FQDN for the Twistlock Console

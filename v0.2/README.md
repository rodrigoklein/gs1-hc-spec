# The Horizontal Communication Standard

The information on this page explain how the horizontal communication works.

### The need

If you are here, probably you are in developing something or you are in charge to manage a traceability project to follow the Brazil Regulation about the SNCM.

Based on the ANVISA´s decision to keep their efforts to handle only the regulatory information about the drug traceability, the market had to find a way to improve the efficiency of the data exchange on the supply chain. 

This search for efficiency, means that we need to have some standard interfaces to provide a faster onboarding of the trading partners in Brazil. If we start looking only on the private market, we have more than 70000 drugstores, 2000 distributors and 400 pharmaceutical companies to connect. It can consume a lot of time (and money) when we look at the common way that the service providers usually use to connect the trading partners.

### What this standard implement

This standard developed by a GS1 Brazil Workgroup developed some common artifacts that enable the interoperability between trading partners. This artifacts are basically a set of Interfaces and Messages that act as a glue between companies in the supply chain.

### What we have inside the HC Stardard?

The standard basically implements a Webservice whith 3 simple methods that allows the data exchange between the companies. In addition we also developed some XML artifacts that can act as an Envelope to provide a standard wey to package and route messages among the supply chain.

### What is the security of the HC Standard?

In the beginning of the work, the workgroup made some assumptions to speedup the development and put the focus on the most important points to work. 

The main assumption were that we do not need stay focused on the technology because it can became an infinite loop. Now a days we have many good alternatives on the market and each member of the group could have their own preferences. 

Based on that, we have decided to keep the same stack that ANVISA is using. With this strategy we can save time discussing the technology and can save a lot of money in terms of software development because, the same developer that need to implement the vertical connection to the SNCM also can develop the horizontal communication.

In this way, we are following the same security stack of the SNCM System that means:

- The use of the SSL (Secure Shell Layer) over HTTP communication.
- Mutual Authentication using the ICP-Brasil Digital certificates
- Electronic Signature on the XML messages to assure the authenticity and integrity of the messages.

![image info](authSchema.png)
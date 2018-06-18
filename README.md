# fabric-business-network

Now that the business network has been defined, it must be packaged into a deployable business network archive (.bna) file.

    Using the command line, navigate to the tutorial-network directory.

    From the tutorial-network directory, run the following command:

    

    composer archive create -t dir -n .

After the command has run, a business network archive file called tutorial-network@0.0.1.bna has been created in the tutorial-network directory.



#Deploying the business network

After creating the .bna file, the business network can be deployed to the instance of Hyperledger Fabric. Normally, information from the Fabric administrator is required to create a PeerAdmin identity, with privileges to install chaincode to the peer as well as start chaincode on the composerchannel channel. However, as part of the development environment installation, a PeerAdmin identity has been created already.

After the business network has been installed, the network can be started. For best practice, a new identity should be created to administer the business network after deployment. This identity is referred to as a network admin.
Retrieving the correct credentials

A PeerAdmin business network card with the correct credentials is already created as part of development environment installation.
Deploying the business network

Deploying a business network to the Hyperledger Fabric requires the Hyperledger Composer business network to be installed on the peer, then the business network can be started, and a new participant, identity, and associated card must be created to be the network administrator. Finally, the network administrator business network card must be imported for use, and the network can then be pinged to check it is responding.

    To install the business network, from the tutorial-network directory, run the following command:

    

    composer network install --card PeerAdmin@hlfv1 --archiveFile tutorial-network@0.0.1.bna

    The composer network install command requires a PeerAdmin business network card (in this case one has been created and imported in advance), and the the file path of the .bna which defines the business network.

    To start the business network, run the following command:

    

    composer network start --networkName tutorial-network --networkVersion 0.0.1 --networkAdmin admin --networkAdminEnrollSecret adminpw --card PeerAdmin@hlfv1 --file networkadmin.card

    The composer network start command requires a business network card, as well as the name of the admin identity for the business network, the name and version of the business network and the name of the file to be created ready to import as a business network card.

    To import the network administrator identity as a usable business network card, run the following command:

    

    composer card import --file networkadmin.card

    The composer card import command requires the filename specified in composer network start to create a card.

    To check that the business network has been deployed successfully, run the following command to ping the network:

    

    composer network ping --card admin@tutorial-network

The composer network ping command requires a business network card to identify the network to ping.


#Generating a REST server

Hyperledger Composer can generate a bespoke REST API based on a business network. For developing a web application, the REST API provides a useful layer of language-neutral abstraction.

    To create the REST API, navigate to the tutorial-network directory and run the following command:

    

    composer-rest-server

    Enter admin@tutorial-network as the card name.

    Select never use namespaces when asked whether to use namespaces in the generated API.

    Select No when asked whether to secure the generated API.

    Select Yes when asked whether to enable event publication.

    Select No when asked whether to enable TLS security.

The generated API is connected to the deployed blockchain and business network.

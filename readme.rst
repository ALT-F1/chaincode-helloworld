////////////////////////////////////////////////////////
Chain code - Hello world  using go and the hyperledger
////////////////////////////////////////////////////////

##############
 How to Use
##############

0. `Go-Install Go language`_
1. Clone the `hyperledger`_ 
2. `Fabric-Install the fabric`_
3. `Fabric-Setup the development environment`_
4. Look at the credentials of Lukas inside the `membersrvc.yaml`_, the user will have to log on to interact with the `hyperledger`_
5. Clone this code `Chaincode-Helloworld`_ into ``<hyperledger directory>/fabric/examples`` 
6. Setup 3 UNSECURED peers (setting up secured peers generate marshalling errors for the moment)
    1. Setup 3 terminals as described in `Writing Building and Running Chaincode in a Development Environment`_
    2. Security Setup 
        0. Start your favorite bash command line, on windows start ``Git bash`` for example 
        1. ``cd <GO PATH>/gopg/src/github.com/hyperledger/fabric/devenv/``
        2. ``vagrant up``
        3. ``vagrant ssh``
        4. ``cd $GOPATH/src/github.com/hyperledger/fabric/``
        5. ``make membersrvc && membersrvc``
    3. Vagrant Terminal 1 (validating peer)
        0. Start your favorite bash command line, on windows start ``Git bash`` for example 
        1. ``cd <GO PATH>/gopg/src/github.com/hyperledger/fabric/devenv/``
        2. ``vagrant ssh``
        3. ``cd $GOPATH/src/github.com/hyperledger/fabric/``
        4. ``make peer``
        5. ``peer node start --peer-chaincodedev``
    4. Vagrant Terminal 2 (chaincode)
        0. Start your favorite bash command line, on windows start ``Git bash`` for example 
        1. ``cd <GO PATH>/gopg/src/github.com/hyperledger/fabric/devenv/``
        2. ``vagrant ssh``
        3. ``cd $GOPATH/src/github.com/hyperledger/fabric/examples/chaincode/go/altf1be/chaincode-helloworld/helloworld``
        4. ``go build && CORE_CHAINCODE_ID_NAME=helloWorld CORE_PEER_ADDRESS=0.0.0.0:30303 ./helloworld``
    5. Vagrant Terminal 3 (Command line interpreter)
        0. Start your favorite bash command line, on windows start ``Git bash`` for example 
        1. ``cd <GO PATH>/gopg/src/github.com/hyperledger/fabric/devenv/``
        2. ``vagrant ssh``
        3. ``$GOPATH/src/github.com/hyperledger/fabric/peer``
        4. ``peer network login lukas``
            1. input the password stored in `membersrvc.yaml`_
        5. deploy the chaincode-helloword ``peer chaincode deploy -p ./helloWorld -c '{"Function":"init", "Args":["noArgsyet"]}' -u lukas`` 
        6. query the chaincode-helloword: ``peer chaincode query -u lukas -l golang -n helloWorld -c '{"Function": "query", "Args": ["b"]}'`` 
        7. ``peer chaincode invoke -l golang -u lukas -n helloWorld -c '{"Function":"invoke", "Args":["noArgsyet"]}'`` 

===========================================================================
Vagrant Terminal 3 (Command line interpreter) - UNSECURED peers (working)
===========================================================================

    go build && CORE_CHAINCODE_ID_NAME=helloWorld CORE_PEER_ADDRESS=0.0.0.0:30303 ./helloworld

    peer network login lukas 

    peer chaincode deploy -n helloWorld -c '{"Function":"init", "Args":["noArgsyet"]}'

    peer chaincode invoke -l golang -n helloWorld -c '{"Function":"invoke", "Args":["noArgsyet"]}'

    peer chaincode query -l golang -n helloWorld -c '{"Function": "quey", "Args": ["b"]}' 

===================================================================================
Vagrant Terminal 3 (Command line interpreter) - SECURED  peers (does not work yet)
===================================================================================

    CORE_SECURITY_ENABLED=true CORE_SECURITY_PRIVACY=true peer chaincode deploy -p ./helloWorld -c '{"Function":"init", "Args":["noArgsyet"]}' -u lukas

    CORE_SECURITY_ENABLED=true CORE_SECURITY_PRIVACY=true peer chaincode query -u lukas -l golang -n helloWorld -c '{"Function": "query", "Args": ["b"]}'

    CORE_SECURITY_ENABLED=true CORE_SECURITY_PRIVACY=true peer chaincode invoke -l golang -u lukas -n helloWorld -c '{"Function":"invoke", "Args":["noArgsyet"]}'

    CORE_SECURITY_ENABLED=true CORE_SECURITY_PRIVACY=true peer chaincode query -l golang -u lukas -n helloWorld -c '{"Function":"query", "Args":["noArgsyet"]}'

########################################
Theory - books
########################################

* Ledger, chaincode
    * Ledger, Protocol Specification : https://github.com/hyperledger/fabric/blob/960db9f57a5e19f1f097741c807c01cdbe86ada6/docs/protocol-spec.md
    * Chaincode APIs: https://github.com/hyperledger/fabric/blob/bf9f05014680ba2872eda3c18e42f742f8050066/docs/API/ChaincodeAPI.md
    * shim package : https://godoc.org/github.com/hyperledger/fabric/core/chaincode/shim
    * hyperledger asset management app: https://github.com/hyperledger/fabric/blob/012384ac7c2e8c16496e3c4f3a4b84cec301aead/examples/chaincode/go/asset_management/app/README.md
* Go language
    * https://golang.org/doc/code.html
    * https://golang.org/doc/effective_go.html
    * https://golang.org/doc/faq
    * https://golang.org/pkg/
    * http://www.golangbootcamp.com/book
    * http://www.golang-book.com/
    * https://github.com/initpy/go-book


-- End of the Document

.. URL Links

.. _hyperledger: https://github.com/hyperledger/hyperledger
.. _Fabric-Setup the development environment: https://github.com/hyperledger/fabric/blob/master/docs/dev-setup/devenv.md
.. _Writing Building and Running Chaincode in a Development Environment: https://github.com/hyperledger/fabric/blob/master/docs/API/SandboxSetup.md
.. _membersrvc.yaml: https://github.com/hyperledger/fabric/blob/master/membersrvc/membersrvc.yaml
.. _Chaincode-Helloworld: https://github.com/ALT-F1/chaincode-helloworld
.. _Fabric-Install the fabric: https://github.com/hyperledger/fabric/blob/master/docs/dev-setup/install.md
.. _Go-Install Go language: https://golang.org/doc/install
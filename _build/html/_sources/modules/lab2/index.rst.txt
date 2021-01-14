Build a Node.js and React app with npm within Jenkins Pipeline
==============================================================

a. Fork the sample repository on GitHub

.. figure:: ./images/00.png
   :alt: forked simple-node-js-react-npm-app repository (on GitHub)


**Jenkins Setup (Linux Machine)**

1. Create a bridge network in Docker

.. code-block:: shell-session

    docker network create jenkins

2. Create the following volumes

.. code-block:: shell-session

    docker volume create jenkins-docker-certs
    docker volume create jenkins-data

3. In order to execute Docker commands inside Jenkins nodes, download and run the docker:dind Docker image

.. code-block:: shell-session

    docker container run --name jenkins-docker --rm --detach \
    --privileged --network jenkins --network-alias docker \
    --env DOCKER_TLS_CERTDIR=/certs \
    --volume jenkins-docker-certs:/certs/client \
    --volume jenkins-data:/var/jenkins_home \
    --volume "$HOME":/home \
    --publish 3000:3000 docker:dind

4. Run the jenkinsci/blueocean image as a container in Docker using the following docker container run command

.. code-block:: shell-session

    docker container run --name jenkins-tutorial --rm --detach \
    --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
    --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
    --volume jenkins-data:/var/jenkins_home \
    --volume jenkins-docker-certs:/certs/client:ro \
    --volume "$HOME":/home --publish 8080:8080 jenkinsci/blueocean

5. Open up following URL in browser localhost:8080
   Setup wizard

.. figure:: ./images/01.png
   :alt: Unlocking Jenkins

6. Creating the first administrator user

.. figure:: ./images/02.png

7. Instance Configuration

.. figure:: ./images/03.png

8. Start using Jenkins

.. figure:: ./images/04.png

9. Create new jobs

.. figure:: ./images/05.png

10. Enter an item name field, specify the name for your new Pipeline project

.. figure:: ./images/06.png

11. Add pipeline description and choose Pipeline script from SCM option.

.. figure:: ./images/07-1.png

12. Open Blue Ocean | click Run, then quickly click the OPEN link which appears briefly at the lower-right to see Jenkins building your Pipeline project

.. figure:: ./images/08.png

13. The Blue Ocean interface turns green if Jenkins built your Node.js and React application successfully.

.. figure:: ./images/10.png

14. Added test stage to Pipeline

.. figure:: ./images/11.png

15. Added a final deliver stage to Pipeline

.. figure:: ./images/12.png

16. React app running on localhost:3000

.. figure:: ./images/13.png

17. Onclick the Proceed button to complete the Pipeline’s execution.

.. figure:: ./images/14.png


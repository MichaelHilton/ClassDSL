# 313-Recitation 2: Docker and Compose
**Goal:** During this recitation, we will make sure everyone is
comfortable with using Docker and show an alternative method for running
Docker containers, using Docker Compose.

**Activity 1: Make sure you can run Mayan EDMS**

Ensure that you can run the Mayan EDMS using the Docker examples
provided at this URL:

<https://docs.mayan-edms.com/topics/docker.html#docker-image>

**Activity 2: Create a Docker Compose configuration for running Mayan
EDMS**

1.  Create a service compose file that will run the required services\
    (mayan-edms and mayan-edms-postgres)\
    <https://docs.docker.com/compose/gettingstarted/#step-3-define-services-in-a-compose-file>

2.  Your compose file must have a section in each service for the
    different parameters used to start the containers, as specified in
    the Mayan EDMS documentation\
    <https://docs.mayan-edms.com/topics/docker.html#docker-image>

    a.  -e is for environment variables, one required for each -e

    b.  -v is for mounted volumes, one required for each -v

    c.  -p is for port forwarding

    d.  a section is required for the restart strategy

    e.  a name must be specified

    f.  an image must be specified

    g.  Hint: the MAYAN\_DATABASE\_HOST value will have to be changed

    h.  Bonus: one container (service) may have to be started before the
        other to prevent a race condition, which? Can you make the
        configuration ensure that happens?

3.  To get credit, submit your docker-compose.yaml in GitHub Classroom.\
    <https://classroom.github.com/a/YDP-HPpu>

**Template to get you started:**

<https://gist.github.com/cmeiklejohn/fa47fd1bc1da638bc49f3e1d342b8d09>

**Goal:** During this recitation, students will learn how to use Gremlin
to run a chaos engineering-style attack against a microservice
application.

**Task:**

1.  Make sure you have \*no\* Docker containers running for PostgreSQL
    or Mayan-EDMS before you start this exercise. Confirm this with
    docker ps and remove any currently running instances of Mayan-EDMS
    and PostgreSQL.

2.  Create an account with Gremlin (http://gremlin.com). When asked for
    the organization and team, enter Carnegie Mellon University for both
    -- it will tell you that permission will be granted by the team
    owner -- I will grant permission.

3.  Start a new instance of the Gremlin-enabled Mayan-EMDS.\
    docker run -d \\\
    -p 8000:8000 \\\
    \--cap-add=NET\_ADMIN \\\
    \--cap-add=SYS\_BOOT \\\
    \--cap-add=SYS\_TIME \\\
    \--cap-add=KILL \\\
    -e GREMLIN\_ORG\_ID=\"80fc5b45-ab32-5544-9f54-071e5d6436af\" \\\
    -e GREMLIN\_ORG\_SECRET=\"b92a9ffb-aa2e-4ee4-aa9f-fbaa2efee449\" \\\
    -it cmeiklejohn/mayanedms:3.2.7

4.  Go to the "Clients" tab in Gremlin and find the identifier for your
    client. You should be able to correlate the container name (see
    using docker ps) and the local-hostname of the container that\'s
    running. For all of the following attacks, target only your
    container and not your classmates, please.

5.  Run your first attack using the Attack tab in the menu:

    a.  Select a State Attack and choose the Attack type of
        \"Shutdown.\"

    b.  What happens to Mayan-EDMS?

    c.  What happens to your container?

6.  Let\'s try another attack, but instead, let\'s simulate an outage
    using an attack.

    d.  Select Scenario.

    e.  Type a name and description of the outage.

    f.  Add an attack: Resource, CPU.

    g.  Scroll back up and create a hypothesis of what you think will
        happen to Mayan.

    h.  What is your hypothesis?

    i.  Run your attack scenario!

    j.  What happened to Mayan-EDMS?

    k.  What happened to your container?

    l.  Was your hypothesis correct?

7.  Terminate your Docker instances. Let\'s try an example using
    Mayan-EDMS with PostgreSQL.

    m.  You may have to adjust the docker-volumes path as you did in
        recitation 2.

    n.  First, run PostgreSQL:\
        docker run -d \\

> -p 5432:5432 \\
>
> -e POSTGRES\_USER=mayan \\
>
> -e POSTGRES\_DB=mayan \\
>
> -e POSTGRES\_PASSWORD=mayanuserpass \\
>
> -v /docker-volumes/mayan-edms/postgres:/var/lib/postgresql/data \\
>
> \--cap-add=NET\_ADMIN \\
>
> \--cap-add=SYS\_BOOT \\
>
> \--cap-add=SYS\_TIME \\
>
> \--cap-add=KILL \\
>
> -e GREMLIN\_ORG\_ID=\"80fc5b45-ab32-5544-9f54-071e5d6436af\" \\
>
> -e GREMLIN\_ORG\_SECRET=\"b92a9ffb-aa2e-4ee4-aa9f-fbaa2efee449\" \\
>
> -it cmeiklejohn/mayanedms-postgresql:9.6

o.  Now, run Mayan-EDMS:\
    docker run \\

> -p 8000:8000 \\

-e MAYAN\_DATABASE\_ENGINE=django.db.backends.postgresql \\

-e MAYAN\_DATABASE\_HOST=172.17.0.1 \\

-e MAYAN\_DATABASE\_NAME=mayan \\

-e MAYAN\_DATABASE\_PASSWORD=mayanuserpass \\

-e MAYAN\_DATABASE\_USER=mayan \\

-e MAYAN\_DATABASE\_CONN\_MAX\_AGE=0 \\

-v /docker-volumes/mayan-edms/media:/var/lib/mayan \\

\--cap-add=NET\_ADMIN \\

\--cap-add=SYS\_BOOT \\

\--cap-add=SYS\_TIME \\

\--cap-add=KILL \\

-e GREMLIN\_ORG\_ID=\"80fc5b45-ab32-5544-9f54-071e5d6436af\" \\

-e GREMLIN\_ORG\_SECRET=\"b92a9ffb-aa2e-4ee4-aa9f-fbaa2efee449\" \\

-it cmeiklejohn/mayanedms:3.2.7

p.  Create a scenario that targets \*only\* PostgreSQL using the
    shutdown attack.

q.  What was your hypothesis?

r.  What happened to Mayan-EDMS?

s.  What happened to PostgreSQL?

t.  What happened to your container?

u.  Was your hypothesis correct?

<!-- -->

8.  **Rerun the previous experiment, but instead, use the following
    command to start PostgreSQL:**

    v.  docker run -d \\

        \--restart=always \\

        -p 5432:5432 \\

        -e POSTGRES\_USER=mayan \\

        -e POSTGRES\_DB=mayan \\

        -e POSTGRES\_PASSWORD=mayanuserpass \\

        -v /docker-volumes/mayan-edms/postgres:/var/lib/postgresql/data
        \\

        \--cap-add=NET\_ADMIN \\

        \--cap-add=SYS\_BOOT \\

        \--cap-add=SYS\_TIME \\

        \--cap-add=KILL \\

        -e GREMLIN\_ORG\_ID=\"80fc5b45-ab32-5544-9f54-071e5d6436af\" \\

        -e GREMLIN\_ORG\_SECRET=\"b92a9ffb-aa2e-4ee4-aa9f-fbaa2efee449\"
        \\

        -it cmeiklejohn/mayanedms-postgresql:9.6

    w.  Create a scenario that targets \*only\* PostgreSQL using the
        shutdown attack.

    x.  What was your hypothesis?

    y.  What happened to Mayan-EDMS?

    z.  What happened to PostgreSQL?

    a.  What happened to your container?

    b.  Was your hypothesis correct?

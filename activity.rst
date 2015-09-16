.. important::
    You are viewing an outdated version of the docs. Please find the latest version `here <http://doc.scrapinghub.com/>`_.

============
Activity Log
============

Scrapinghub keeps track of certain project events such as when spiders are run
or new spiders are deployed. This activity log can be accessed in :doc:`dash` by
clicking on **Activity** in the left sidebar, or programmatically through the
:ref:`activity-api` described below.

.. _activity-api:

Activity API
------------

The *Activity API* collects messages for each project and returns them in reverse order
that they were posted. It supports a ``count`` parameter to get the most recent N posts.

For example::

    $ curl -d '{"foo": 2}' https://storage.scrapinghub.com/activity/1111111/
    $ curl -d '{"foo": 3}' https://storage.scrapinghub.com/activity/1111111/
    $ curl -d '{"foo": 4}' https://storage.scrapinghub.com/activity/1111111/
    $ curl https://storage.scrapinghub.com/activity/1111111/?count=2
    {"foo":4}
    {"foo":3}

You can also get activity across multiple projects::

    $ curl -d '{"bar": 1}' https://storage.scrapinghub.com/activity/2222222/
    $ curl https://storage.scrapinghub.com/activity/projects/?pcount=1&meta=_project&p=1111111&p=2222222
    {"_project": 2222222, "bar": 1}
    {"_project": 1111111, "foo": 4}

As you can see, the ``count`` parameter is per project. A ``p`` parameter, which can be repeated, may be used to specify the projects, and the meta parameter ``_project`` can be used to put the project ID in the results. The number of results can be controlled by a ``count`` parameter, and the number of results per project can be limited by ``pcount`` parameter.


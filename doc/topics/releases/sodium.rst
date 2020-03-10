:orphan:

====================================
Salt Release Notes - Codename Sodium
====================================


Salt mine updates
=================

Syntax update
-------------

The syntax for defining salt functions in config or pillar files has changed to
also support the syntax used in :py:mod:`module.run <salt.states.module.run>`.
The old syntax for the mine_function - as a dict, or as a list with dicts that
contain more than exactly one key - is still supported but discouraged in favor
of the more uniform syntax of module.run.

Minion-side ACL
---------------

Salt has had master-side ACL for the salt mine for some time, where the master
configuration contained `mine_get` that specified which minions could request
which functions. However, now you can specify which minions can access a function
in the salt mine function definition itself (or when calling :py:func:`mine.send <salt.modules.mine.send>`).
This targeting works the same as the generic minion targeting as specified
:ref:`here <targeting>`. The parameters used are ``allow_tgt`` and ``allow_tgt_type``.
See also :ref:`the documentation of the Salt Mine <mine_minion-side-acl>`.

State Execution Module
============================================

The :mod:`state.test <salt.modules.state.test>` function
can be used to test a state on a minion. This works by executing the
:mod:`state.apply <salt.modules.state.apply>` function while forcing the ``test`` kwarg
to ``True`` so that the ``state.apply`` function is not required to be called by the
user directly. This also allows you to add the ``state.test`` function to a minion's 
``minion_blackout_whitelist`` pillar if you wish to be able to test a state while a
minion is in blackout.

===========================
Chapter 5: Connect the dots
===========================

In this chapter, we'll add business logic to the models to automate the processes of our application
and turn it into a dynamic and useful tool. This will involve defining actions, constraints,
automatic computations, and other model methods.

.. todo: explain the env (self.env.uid, self.env.user, self.env.ref(xml_id), self.env[model_name])
.. todo: explain magic commands
.. todo: 6,0,0 to associate tags to properties in data
.. todo: create (create offer -> offer received state) and write methods
.. todo: auto-update property state based on received offers state (write)
.. todo: best offer stat button
.. todo: accepting offer refuses others

.. _tutorials/server_framework_101/computed_fields:

Computed fields
===============

.. todo: change section title

**Computed fields** are a special type of field that derive their value through programmatic
computation rather than direct storage. The computation is performed on-the-fly by the server
whenever the field is accessed. This makes computed fields highly convenient for tasks like
displaying the results of calculations directly in views, automating repetitive processes, or
assisting users with data entry.

In Odoo, computed fields are implemented by defining a specific Python method and linking it to a
field declaration using the `compute` argument. This method operates on a **recordset** :dfn:`a
collection of records from the same model` represented by the `self` argument of the compute method.
The method must iterate over the records to compute and set the field's value for each record.

.. todo: ref on recordsets
.. todo: compute (offer deadline)
.. todo: For relational fields, it’s possible to use paths through a field as a dependency: @api.depends('partner_id.name')
.. todo: methods are private by default, meaning that they can't be called from the presentation
         tier, only from the business tier. See chap 1
.. todo: Although relational field names end with the `_id` or `_ids` suffix, variables holding a recordset of such fields
         are typically not suffixed. That is because, while the field represents the referenced record's id that is stored in the
         database, the variable is holding the full record in memory.

.. _tutorials/server_framework_101/inverse_computed_fields:

Inverse computed fields
-----------------------

You might have noticed that computed fields are read-only by default. This is expected since the
user is not supposed to set a value by themselves.

.. todo: change section title

tmp

.. todo: inverse (offer deadline)

.. _tutorials/server_framework_101/related_fields:

Related fields
--------------

.. todo: change section title

tmp

.. todo: related fields (buyer's phone)

.. _tutorials/server_framework_101/stored_computed_fields:

Stored computed fields
----------------------

.. todo: change section title

When the computation depends on other fields, the method should be decorated with
:code:`@api.depends()`, which specifies the fields that trigger an automatic recomputation whenever
their value changes.

.. todo: implement search method

.. _tutorials/server_framework_101/onchanges:

Onchange methods
================

.. todo: change section title

**Onchange methods** are a feature of the server framework designed to respond to changes in field
values directly within the user interface. They are executed when a user modifies a field in a form
view, even before saving the record to the database. This allows for real-time updates of other
fields and provides immediate user feedback, such as blocking user errors, non-blocking warnings, or
suggestions. However, because onchange methods are only triggered by changes made in the UI,
specifically from a form view, they are best suited for assisting with data entry and providing
feedback, rather than implementing core business logic in a module.

In Odoo, onchange methods are implemented as Python methods and linked to one or more fields using
the :code:`@api.onchange()` decorator. These methods are triggered when the specified fields' values
are altered. They operate on the in-memory representation of a single-record recordset received
through `self`. If field values are modified, the changes are automatically reflected in the UI.

.. todo: raise UserError + translation
.. todo: if garden checked -> show and compute total area

.. _tutorials/server_framework_101/constraints:

Constraints
===========

.. todo: change section title

**Constraints** are rules that enforce data integrity by validating field values and relationships
between records. They ensure that the data stored in your application remains consistent and meets
business requirements, preventing invalid values, duplicate entries, or inconsistent relationships
from being saved to the database.

In Odoo, constraints can be implemented at two different levels: directly in the database schema
using **SQL constraints**, or in the model's logic using **Python constraints**. Each type has its
own advantages and use cases, allowing developers to choose the most appropriate validation method
based on their specific needs.

.. _tutorials/server_framework_101/sql_constraints:

SQL constraints
---------------

SQL constraints are database-level rules that are enforced directly by PostgreSQL when records are
created or modified. They are highly efficient in terms of performance, but they cannot handle
complex logic or access individual records. As a result, they are best suited for straightforward
use cases, such as ensuring that a field value is unique or falls within a specific range.

SQL constraints are defined in the model using the `_sql_constraints` class attribute. This
attribute contains a list of tuples, with each tuple specifying the constraint's name, the SQL
expression to validate, and the error message to display if the constraint is violated.

.. todo: price more than zero
.. todo: unique tag constraint

.. _tutorials/server_framework_101/python_constraints:

Python constraints
------------------

..  They are less performant than SQL constraints, but can handle business logic and have access to records.
    Executed when?

Python constraints are record-level rules implemented through Python methods defined on the model.
Unlike SQL constraints, they allow for flexible and context-aware validations based on business
logic, at the expense of higher performance impact than SQL constraints, as they are evaluated
server-side on recordsets. Use cases include ensuring that certain fields align with a specific
condition or that multiple fields work together in a valid combination.

Python constraints are defined in the model as methods decorated with :code:`@api.constrains()`,
which specifies the fields that trigger the validation. These methods are triggered automatically
when a record is created or updated, performing custom validation and raising validation errors if
the constraint is violated.

.. todo: accept only one offer

.. _tutorials/server_framework_101/defaults:

Defaults
========

.. todo: change section title
.. todo: introduce lambda functions and fields.Date.today for defaults :point_down:
   also mention that `self` is evaluated as the current recordset in lambda functions

There is a problem with the way we defined our `Date` fields in the previous chapters: their default value relies on
:code:`fields.Date.today()` or some other static method. When the code is loaded into memory, the date is
computed once and reused for all newly created records until the server is shut down. You probably didn't
notice it, unless you kept your server running for several days, but it would be much more visible with
`Datetime` fields, as all newly created records would share the same timestamp.

That's where lambda functions come in handy. As they generate an anonymous function each time they're evaluated
at runtime, they can be used in the computation of default field values to return an updated value for each new record.

.. todo: salesperson_id = fields.Many2one(default=lambda self: self.env.user)
.. todo: real.estate.offer.amount::default -> property.selling_price (add related?)
.. todo: real.estate.tag.color -> default=_default_color ;  def _default_color(self): return random.randint(1, 11)  (check if lambda works)
.. todo: copy=False on some fields

.. _tutorials/server_framework_101/actions:

Actions
=======

.. todo: change section title
.. todo: "assign myself as salesperson" action
.. todo: "view best offer" statbutton
.. todo: accept/refuse offer buttons
.. todo: action name=...

tmp

.. _tutorials/server_framework_101/action_object:

Object
------

tmp

.. _tutorials/server_framework_101/action_name:

Name
----

tmp

.. _tutorials/server_framework_101/shell:

Shell
=====

.. todo: change section title

tmp

----

.. todo: add incentive for chapter 6

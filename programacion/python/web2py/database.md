web2py uses a Database Abstraction Layer (DAL) instead of an Object Relational Mapper (ORM). From a conceptual point of view, this means that different database tables are mapped into different instances of one Table class and not into different classes, while records are mapped into instances of one Row class, not into instances of the corresponding table class. From a practical point of view, it means that SQL syntax maps almost one-to-one into DAL syntax, and there is no complex metaclass programming going on under the hood as in popular ORMs, which would add latency.
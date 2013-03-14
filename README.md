Django Dynamic Legacy Models
============================

Dynamic Model Generator which can be used when working with legacy databases. This is based on django's inspectdb.

Installation:
---------------------------
`pip install -e git+https://github.com/rodxavier/django-dynamic-legacy-models.git#egg=dlm`

Sample Usage:
----------------------------
1. Modify INSTALLED_APPS in your settings and add the `dlm` app.

2. Edit the models.py where you want to place the dynamic legacy models and add these lines.
  
    #### Without table_name_filter
    
        from dlm.model_generator import ModelGenerator
        
        gen = ModelGenerator('db_key', globals())
        gen.generate_models()
        
    #### With table_name_filter
    
        from dlm.model_generator import ModelGenerator
        
        gen = ModelGenerator('db_key', globals(), table_name_filter=lambda x: x.startswith('dlm'))
        gen.generate_models()
        
3. Now you can access your legacy tables using Django's ORM.

    #### Example for a table named legacy_database_table
        from <app>.models import <LegacyDatabaseTable>


####NOTE: 
- The db_key param is the key used in the DATABASES setting.
- You can also pass a keyword argument table_name_filter which should be a function taking one parameter and returning a boolean. The table_name_filter is useful when you don't want all of the tables in the legacy db to be converted to django models.
- This currently does not work with tables having composite keys and tables without primary keys.
    

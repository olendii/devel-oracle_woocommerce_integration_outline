# Oracle and WooCommerce integration outline

### Notes.
I used Oracle 11g XE and deprecated [WooCommerce API](http://woocommerce.github.io/woocommerce-rest-api-docs/v3.html)

### Preparing Oracle Database.
1. [Install APEX](https://oracle-base.com/articles/misc/oracle-application-express-apex-5-0-installation).
2. Grant privileges.

```plpgsql
    grant execute on sys.dbms_crypto to username;
    grant execute on sys.utl_http to username;
    grant execute on sys.dbms_lock to username;
```

3. Create ACL.

```plpgsql
    BEGIN
      DBMS_NETWORK_ACL_ADMIN.create_acl (
        acl           => 'site_acl_file.xml',
        description   => 'ACL for admin',
        principal     => 'user_name',
        is_grant      => TRUE,
        privilege     => 'connect',
        start_date    => NULL,
        end_date      => NULL);
    END;

    BEGIN
      DBMS_NETWORK_ACL_ADMIN.assign_acl (
        acl          => 'site_acl_file.xml',
        HOST         => 'site.com',
        lower_port   => 80,
        upper_port   => 80);
    END;
```
... to be continue.

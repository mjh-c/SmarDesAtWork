# Installation Notes for Use Case 5
Follow these steps to start the SmartDevices-Gatweway for the Use Case 5 Sample:

# 1. General

 * Setup the services as described in [Installation](../../installation.md)

# 2. smardes-middleware

## 2.1  Copy Config into smardes-middleware

* Copy the whole content of `uc5/smardes-middleware/` into `smardes-middleware-x.y.z\smardes-backend-services-x.y.z`

## 2.2 Database Setup

### 2.2.1 Copy JDBC Driver for your database

* ... into `smardes-backend-services-x.y.z\externaldb\lib`

For example, for MS SQL Database this would be sqljdbc42.jar.

### 2.2.2 Modify externaldb/META-INF/persistence.xml

   * Add the following entry:
```
	<persistence-unit name="uc5">
		<properties>
			<property name="hibernate.ejb.cfgfile" value="/hibernate_uc5.cfg.xml"/>
		</properties>
	</persistence-unit>
```

### 2.2.3 Configure externaldb/hibernate_uc5.cfg.xml

   * Adjust DB Configuration, notably:
   ```
   hibernate.connection.url
   hibernate.connection.username
   hibernate.connection.password
   ```

### 2.2.4 Adjust config/queries/uc5.properties

   * Might be needed to add a prefix to the table, e.g. schema name or similar.


## 2.3 Other configurations

```
 config/dbmon/uc5.properties:
 dbmon.uc5.interval
```

# 3. smartdevices-gateway

  * Copy the whole content of `uc5/smartdevices-gateway/config/` into `smartdevices-gateway/config/`
  * Start the smartdevices-gateway
    * Check if smartdevices-gateway is accessable via swagger:
         > http://localhost:7000/swagger/index.html

# 4. smartdevices-app

  * Configure the Settings in the Client-Application:
    * `Server Address` - Url to the Server installation like "http://192.168.0.1"
    * `Server Port` - Port of the Server
    * `Username` - A valid Username
      * Pick a Username from the Configuration File `smartdevices-gateway/config/UserConfig.json`
      * In this Example one of
         ```
            operator1
            operator2
            operator3
            operator4
         ```
    * `Device Id` - A valid Device-Id
      * Convention: For all phones and tablets "A", for all watches "B".

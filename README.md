# SSO Application


## Users and Roles in the Application

| User | Role |
| :--- | :--- |
| **Amar** | Owner |
| **Admin** | Admin |
| **Suresh** | Manager |
| **Sagar** | Authenticated User |
| **Unauthenticated User** | Unauthenticated User |




### Production Grade LDIF File
A "production grade" LDIF file goes beyond a simple demonstration by incorporating best practices for security, scalability, and maintainability. This includes using hashed passwords, a well-defined hierarchical structure, and clear documentation.

#### Key Features of this Production-Ready LDIF:

1. **Hashed Passwords** (`userPassword`): Passwords are not stored in plaintext. They are stored as securely hashed values (e.g., using the SSHA algorithm). You must replace the `GENERATED_HASH` placeholders with hashes for your specific passwords.

2. **Clear Hierarchy**: The file establishes a clear separation between users and roles by using different organizational units (`ou=users` and `ou=roles`).

3. **Descriptive Attributes:** It includes attributes like `givenName` and `description` for better clarity and management.

4. **Role-Based Access Control (RBAC):** Roles are defined as `groupOfNames` entries, and users are added as members. This is the standard, scalable method for managing permissions in LDAP.

### How to Use This LDIF
**Generate Hashed Passwords:** Do NOT use the placeholder passwords. Use a tool like `slappasswd` (included with OpenLDAP) to generate SSHA hashes for each password. For example:


```bash
slappasswd -h {SSHA} -s "your_password_here"
```
Replace `GENERATED_HASH` in the LDIF file with the output of this command.

**Update the Base DN:** The file uses `dc=example,dc=org` as a placeholder for the domain. You must replace this with your actual domain components (e.g., `dc=yourcompany,dc=org`).

**Load the File:** Once the file is updated, you can load it into your LDAP directory using a tool like `ldapadd`:


```bash
ldapadd -x -W -D "cn=admin,dc=example,dc=org" -f your_file_name.ldif
```

### Production LDIF File Content

```ldif
#
# Complete and Combined LDIF File for the LDAP Directory
#
# This file includes all organizational units, user accounts, and
# group-based roles discussed.
#
# Base DN: dc=example,dc=org
#

#
# Organizational Units (OUs) - The Top-Level Containers
#
dn: ou=people,dc=example,dc=org
objectClass: organizationalUnit
ou: people
description: Container for all user accounts.

dn: ou=groups,dc=example,dc=org
objectClass: organizationalUnit
ou: groups
description: Container for all roles and groups.

dn: ou=engineering,ou=people,dc=example,dc=org
objectClass: organizationalUnit
ou: engineering
description: Members of the engineering team.

dn: ou=sales,ou=people,dc=example,dc=org
objectClass: organizationalUnit
ou: sales
description: Members of the sales team.


#
# User Accounts - All users are listed here with their attributes
#
# Engineer - Jane Doe
dn: uid=jdoe,ou=engineering,ou=people,dc=example,dc=org
objectClass: inetOrgPerson
objectClass: posixAccount
uid: jdoe
givenName: Jane
sn: Doe
cn: Jane Doe
mail: jdoe@example.org
userPassword:: e1NTSEF9V09zOEp2aGFWNUZlWFFXSDJraG81aGF5V1JzL2F2QkY=
title: Senior Software Engineer
employeeNumber: 1001
telephoneNumber: +1 555-123-4567
uidNumber: 1001
gidNumber: 500
homeDirectory: /home/jdoe
gecos: Jane Doe, Software Engineering, Ext. 4567

# Engineer - Michael Chen
dn: uid=mchen,ou=engineering,ou=people,dc=example,dc=org
objectClass: inetOrgPerson
objectClass: posixAccount
uid: mchen
givenName: Michael
sn: Chen
cn: Michael Chen
mail: mchen@example.org
userPassword:: e1NTSEF9V09zOEp2aGFWNUZlWFFXSDJraG81aGF5V1JzL2F2QkY=
title: Software Engineer
employeeNumber: 1002
telephoneNumber: +1 555-234-5678
uidNumber: 1002
gidNumber: 500
homeDirectory: /home/mchen
gecos: Michael Chen, Software Engineering, Ext. 5678

# Engineer - Emily Johnson
dn: uid=ejohnson,ou=engineering,ou=people,dc=example,dc=org
objectClass: inetOrgPerson
objectClass: posixAccount
uid: ejohnson
givenName: Emily
sn: Johnson
cn: Emily Johnson
mail: ejohnson@example.org
userPassword:: e1NTSEF9V09zOEp2aGFWNUZlWFFXSDJraG81aGF5V1JzL2F2QkY=
title: Software Engineer Intern
employeeNumber: 1003
telephoneNumber: +1 555-345-6789
uidNumber: 1003
gidNumber: 500
homeDirectory: /home/ejohnson
gecos: Emily Johnson, Software Engineering, Ext. 6789

# Sales - Alex Rodriguez
dn: uid=arodriguez,ou=sales,ou=people,dc=example,dc=org
objectClass: inetOrgPerson
objectClass: posixAccount
uid: arodriquez
givenName: Alex
sn: Rodriguez
cn: Alex Rodriguez
mail: arodriquez@example.org
userPassword:: e1NTSEF9V09zOEp2aGFWNUZlWFFXSDJraG81aGF5V1JzL2F2QkY=
title: Regional Sales Manager
employeeNumber: 2001
telephoneNumber: +1 555-987-6543
uidNumber: 2001
gidNumber: 501
homeDirectory: /home/arodriguez
gecos: Alex Rodriguez, Sales, Ext. 7654

# Sales - Sarah Lee
dn: uid=slee,ou=sales,ou=people,dc=example,dc=org
objectClass: inetOrgPerson
objectClass: posixAccount
uid: slee
givenName: Sarah
sn: Lee
cn: Sarah Lee
mail: slee@example.org
userPassword:: e1NTSEF9V09zOEp2aGFWNUZlWFFXSDJraG81aGF5V1JzL2F2QkY=
title: Sales Representative
employeeNumber: 2002
telephoneNumber: +1 555-876-5432
uidNumber: 2002
gidNumber: 501
homeDirectory: /home/slee
gecos: Sarah Lee, Sales, Ext. 5432

# Sales - David Wong
dn: uid=dwong,ou=sales,ou=people,dc=example,dc=org
objectClass: inetOrgPerson
objectClass: posixAccount
uid: dwong
givenName: David
sn: Wong
cn: David Wong
mail: dwong@example.org
userPassword:: e1NTSEF9V09zOEp2aGFWNUZlWFFXSDJraG81aGF5V1JzL2F2QkY=
title: Sales Representative
employeeNumber: 2003
telephoneNumber: +1 555-765-4321
uidNumber: 2003
gidNumber: 501
homeDirectory: /home/dwong
gecos: David Wong, Sales, Ext. 4321

# Owner - Amar
dn: uid=amar,ou=people,dc=example,dc=org
objectClass: inetOrgPerson
objectClass: posixAccount
uid: amar
givenName: Amar
sn: User
cn: Amar User
mail: amar@example.org
userPassword:: {SSHA}n9sK68GvR/22WwY9M8Uf+3N+1Xo2hQ==
uidNumber: 1004
gidNumber: 500
homeDirectory: /home/amar

# Admin - Madmin
dn: uid=madmin,ou=people,dc=example,dc=org
objectClass: inetOrgPerson
objectClass: posixAccount
uid: madmin
givenName: Madmin
sn: User
cn: Madmin User
mail: madmin@example.org
userPassword:: {SSHA}n9sK68GvR/22WwY9M8Uf+3N+1Xo2hQ==
uidNumber: 1005
gidNumber: 500
homeDirectory: /home/madmin

# Manager - Suresh
dn: uid=suresh,ou=people,dc=example,dc=org
objectClass: inetOrgPerson
objectClass: posixAccount
uid: suresh
givenName: Suresh
sn: User
cn: Suresh User
mail: suresh@example.org
userPassword:: {SSHA}n9sK68GvR/22WwY9M8Uf+3N+1Xo2hQ==
uidNumber: 1006
gidNumber: 500
homeDirectory: /home/suresh

# Authenticated User - Sagar
dn: uid=sagar,ou=people,dc=example,dc=org
objectClass: inetOrgPerson
objectClass: posixAccount
uid: sagar
givenName: Sagar
sn: User
cn: Sagar User
mail: sagar@example.org
userPassword:: {SSHA}n9sK68GvR/22WwY9M8Uf+3N+1Xo2hQ==
uidNumber: 1007
gidNumber: 500
homeDirectory: /home/sagar


#
# Roles (Groups) - All groups with their respective members
#
# Owner role
dn: cn=Owner,ou=groups,dc=example,dc=org
objectClass: groupOfNames
cn: Owner
description: Users with full ownership rights.
member: uid=amar,ou=people,dc=example,dc=org

# Admin role
dn: cn=Admin,ou=groups,dc=example,dc=org
objectClass: groupOfNames
cn: Admin
description: Users with administrative permissions.
member: uid=madmin,ou=people,dc=example,dc=org

# Manager role
dn: cn=Manager,ou=groups,dc=example,dc=org
objectClass: groupOfNames
cn: Manager
description: Users with managerial permissions.
member: uid=suresh,ou=people,dc=example,dc=org

# Engineering group
dn: cn=Engineering,ou=groups,dc=example,dc=org
objectClass: groupOfNames
cn: Engineering
description: Members of the engineering team.
member: uid=jdoe,ou=engineering,ou=people,dc=example,dc=org
member: uid=mchen,ou=engineering,ou=people,dc=example,dc=org
member: uid=ejohnson,ou=engineering,ou=people,dc=example,dc=org

# Sales group
dn: cn=Sales,ou=groups,dc=example,dc=org
objectClass: groupOfNames
cn: Sales
description: Members of the sales team.
member: uid=arodriguez,ou=sales,ou=people,dc=example,dc=org
member: uid=slee,ou=sales,ou=people,dc=example,dc=org
member: uid=dwong,ou=sales,ou=people,dc=example,dc=org

# Sales Manager role
dn: cn=Sales_Manager,ou=groups,dc=example,dc=org
objectClass: groupOfNames
cn: Sales_Manager
description: Users with sales manager permissions.
member: uid=arodriguez,ou=sales,ou=people,dc=example,dc=org

# All Authenticated users
dn: cn=Authenticated,ou=groups,dc=example,dc=org
objectClass: groupOfNames
cn: Authenticated
description: All users who have successfully authenticated.
member: uid=jdoe,ou=engineering,ou=people,dc=example,dc=org
member: uid=mchen,ou=engineering,ou=people,dc=example,dc=org
member: uid=ejohnson,ou=engineering,ou=people,dc=example,dc=org
member: uid=arodriguez,ou=sales,ou=people,dc=example,dc=org
member: uid=slee,ou=sales,ou=people,dc=example,dc=org
member: uid=dwong,ou=sales,ou=people,dc=example,dc=org
member: uid=amar,ou=people,dc=example,dc=org
member: uid=madmin,ou=people,dc=example,dc=org
member: uid=suresh,ou=people,dc=example,dc=org
member: uid=sagar,ou=people,dc=example,dc=org
```


### Create Spring boot application

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.5.0</version> <!-- corrected version -->
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

	<groupId>com.springboot.keycloak.example.app</groupId>
	<artifactId>springboot-keycloak-app</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>Springboot and Keycloak App</name>
	<description>Demo project for Spring Boot</description>
	<properties>
		<java.version>17</java.version>
	</properties>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter</artifactId>
		</dependency>

        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-actuator</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
        </dependency>

        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <scope>provided</scope>
        </dependency>

        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
            <scope>compile</scope>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-oauth2-resource-server</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>jakarta.persistence</groupId>
            <artifactId>jakarta.persistence-api</artifactId>
        </dependency>

        <dependency>
            <groupId>org.keycloak</groupId>
            <artifactId>keycloak-spring-boot-starter</artifactId>
            <version>24.0.2</version>
        </dependency>

        <dependency>
            <groupId>org.keycloak</groupId>
            <artifactId>keycloak-admin-client</artifactId>
            <version>24.0.2</version>
        </dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>

```


#### Create java application
`SpringbootKeycloakApplication.java`
```java
package com.springboot.keycloak.example.app;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringbootKeycloakApplication {

	public static void main(String[] args) {
		SpringApplication.run(SpringbootKeycloakApplication.class, args);
	}

}
```


#### Create Controllers
`OrderController.java`
```java
package com.springboot.keycloak.example.app.controller;

import java.util.List;

import com.springboot.keycloak.example.app.entity.Order;
import com.springboot.keycloak.example.app.entity.OrderItem;
import com.springboot.keycloak.example.app.repository.OrderItemRepository;
import com.springboot.keycloak.example.app.repository.OrderRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;


@RestController
@RequestMapping("/order")
public class OrderController {
	
	@Autowired
    OrderRepository orderRepository;
	
	@Autowired
    OrderItemRepository orderItemRepository;
	
	@GetMapping
	@RequestMapping("/{restaurantId}/list")
	// manager can access (suresh)
	public List<Order> getOrders(@PathVariable Long restaurantId) {
		return orderRepository.findByRestaurantId(restaurantId);
    }
	
	@GetMapping
	@RequestMapping("/{orderId}")
	// manager can access (suresh)
	public Order getOrderDetails(@PathVariable Long orderId) {
		Order order = orderRepository.findById(orderId).get();
        order.setOrderItems(orderItemRepository.findByOrderId(order.getId()));
        return order;
    }
	
	@PostMapping
	// authenticated users can access
	public Order createOrder(Order order) {
		orderRepository.save(order);
        List<OrderItem> orderItems = order.getOrderItems();
        orderItems.forEach(orderItem -> {
            orderItem.setOrderId(order.id);
            orderItemRepository.save(orderItem);
        });
        return order;
    }

}
```


`RestaurantController.java`
```java
package com.springboot.keycloak.example.app.controller;

import java.math.BigDecimal;
import java.util.List;
import java.util.Optional;

import com.springboot.keycloak.example.app.entity.Menu;
import com.springboot.keycloak.example.app.entity.MenuItem;
import com.springboot.keycloak.example.app.entity.Restaurant;
import com.springboot.keycloak.example.app.repository.MenuItemRepository;
import com.springboot.keycloak.example.app.repository.MenuRepository;
import com.springboot.keycloak.example.app.repository.RestaurantRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;


@RestController
@RequestMapping("/restaurant")
public class RestaurantController {
	
	@Autowired
    RestaurantRepository restaurantRepository;
	
	@Autowired
    MenuRepository menuRepository;
	
	@Autowired
    MenuItemRepository menuItemRepository;

	@GetMapping
	@RequestMapping("/public/list")
	//Public API
	public List<Restaurant> getRestaurants() {
        return restaurantRepository.findAll();
    }
	
	@GetMapping
	@RequestMapping("/public/menu/{restaurantId}")
	//Public API
	public Menu getMenu(@PathVariable Long restaurantId) {
        Menu menu = menuRepository.findByRestaurantId(restaurantId);
        menu.setMenuItems(menuItemRepository.findAllByMenuId(menu.id));
        return menu;
    }
	
	@PostMapping
	// admin can access (admin)
	public Restaurant createRestaurant(Restaurant restaurant) {
        return restaurantRepository.save(restaurant);
    }
	
	@PutMapping
	// manager can access (suresh)
	public Restaurant updateRestaurant(Restaurant restaurant) {
        return restaurantRepository.save(restaurant);
    }
	
	@PostMapping
	@RequestMapping("/menu")
	// manager can access (suresh)
	public Menu createMenu(Menu menu) {
		menuRepository.save(menu);
        menu.getMenuItems().forEach(menuItem -> {
            menuItem.setMenuId(menu.id);
            menuItemRepository.save(menuItem);
        });
        return menu;
    }
	
	@PutMapping
	@RequestMapping("/menu/item/{itemId}/{price}")
	// owner can access (amar)
	public MenuItem updateMenuItemPrice(@PathVariable("itemId") Long itemId
            , @PathVariable("price") BigDecimal price) {
        Optional<MenuItem> menuItem = menuItemRepository.findById(itemId);
        menuItem.get().setPrice(price);
        menuItemRepository.save(menuItem.get());
        return menuItem.get();
    }
}
```


#### Create DTO's

`Role.java`
```java
package com.springboot.keycloak.example.app.dto;

import lombok.Data;

@Data
public class Role {
	private String id;
	private String name;
}
```


`User.java`
```java
package com.springboot.keycloak.example.app.dto;

import lombok.Data;

@Data
public class User {
	
	private String id;

	private String firstName;
	
	private String lastName;
	
	private String email;
	
	private String userName;
	
	private String password;

}
```


#### Create Entities's
`Menu.java`
```java

package com.springboot.keycloak.example.app.entity;

import java.util.List;

import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.Id;
import jakarta.persistence.Table;
import jakarta.persistence.Transient;
import lombok.Getter;
import lombok.RequiredArgsConstructor;
import lombok.Setter;
import lombok.ToString;

@Getter
@Setter
@ToString
@RequiredArgsConstructor
@Entity
@Table(name = "menu")
public class Menu {

    @Id
    @GeneratedValue
    public Long id;

    private Long restaurantId;

    private Boolean active;

    @Transient
    private List<MenuItem> menuItems;    
}

```

`MenuItem.java`
```java
package com.springboot.keycloak.example.app.entity;

import jakarta.persistence.*;
import lombok.Getter;
import lombok.Setter;

import java.math.BigDecimal;

@Getter
@Setter
@Entity
@Table(name = "menu_item")
public class MenuItem {

    @Id
    @GeneratedValue
    public Long id;

    private Long menuId;

    private String name;

    private String description;

    @Column(name = "type_name")
    private String type;

    @Column(name = "group_name")
    private String group;

    private BigDecimal price;

}
```

`Order.java`
```java
package com.springboot.keycloak.example.app.entity;

import java.math.BigDecimal;
import java.util.List;

import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.Table;
import jakarta.persistence.Transient;
import lombok.Getter;
import lombok.RequiredArgsConstructor;
import lombok.Setter;
import lombok.ToString;

@Getter
@Setter
@ToString
@RequiredArgsConstructor
@Entity
@Table(name = "order")
public class Order {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    public Long id;

    private Long restaurantId;

    private BigDecimal total;

    @Transient
    private List<OrderItem> orderItems;
}
```

`OrderItem.java`
```java
package com.springboot.keycloak.example.app.entity;

import java.math.BigDecimal;

import jakarta.persistence.*;
import lombok.Getter;
import lombok.RequiredArgsConstructor;
import lombok.Setter;
import lombok.ToString;

@Getter
@Setter
@ToString
@RequiredArgsConstructor
@Entity
@Table(name = "order_item")
public class OrderItem {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    public Long id;

    private Long orderId;

    private Long menuItemId;

    private BigDecimal price;

}
```


`Restaurant.java`
```java
package com.springboot.keycloak.example.app.entity;

import jakarta.persistence.*;
import lombok.Getter;
import lombok.RequiredArgsConstructor;
import lombok.Setter;
import lombok.ToString;


@Getter
@Setter
@ToString
@RequiredArgsConstructor
@Entity
@Table(name = "restaurant")
public class Restaurant {
    @Id
    @GeneratedValue
    public Long id;

    private String name;

    private String location;

    @Column(name = "type_name")
    private String type;
}

```

#### Create Repositories

`MenuItemRepository.java`
```java
package com.springboot.keycloak.example.app.repository;

import java.util.List;

import com.springboot.keycloak.example.app.entity.MenuItem;
import org.springframework.data.jpa.repository.JpaRepository;


public interface MenuItemRepository extends JpaRepository<MenuItem, Long>{

	List<MenuItem> findAllByMenuId(Long id);

}
```



`MenuRepository.java`
```java
package com.springboot.keycloak.example.app.repository;

import com.springboot.keycloak.example.app.entity.Menu;
import org.springframework.data.jpa.repository.JpaRepository;


public interface MenuRepository  extends JpaRepository<Menu, Long>{

	Menu findByRestaurantId(Long restaurantId);
}
```


`OrderItemRepository.java`
```java
package com.springboot.keycloak.example.app.repository;

import java.util.List;

import com.springboot.keycloak.example.app.entity.OrderItem;
import org.springframework.data.jpa.repository.JpaRepository;


public interface OrderItemRepository extends JpaRepository<OrderItem, Long>{

	List<OrderItem> findByOrderId(Long id);

}
```


`OrderRepository.java`
```java
package com.springboot.keycloak.example.app.repository;

import java.util.List;

import com.springboot.keycloak.example.app.entity.Order;
import org.springframework.data.jpa.repository.JpaRepository;


public interface OrderRepository extends JpaRepository<Order, Long>{

	List<Order> findByRestaurantId(Long restaurantId);

}
```

`RestaurantRepository.java`
```java
package com.springboot.keycloak.example.app.repository;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

import com.springboot.keycloak.example.app.entity.Restaurant;


@Repository
public interface RestaurantRepository extends JpaRepository<Restaurant, Long>{
    
}
```

#### Create security components
`KeycloakSecurityUtil.java`
```java
package com.springboot.keycloak.example.app.security;

import org.keycloak.admin.client.Keycloak;
import org.keycloak.admin.client.KeycloakBuilder;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class KeycloakSecurityUtil {
	
	Keycloak keycloak;
	
	@Value("${keycloak.server-url}")
	private String serverUrl;
	
	@Value("${keycloak.realm}")
	private String realm;
	
	@Value("${keycloak.client-id}")
	private String clientId;
	
	@Value("${keycloak.grant-type}")
	private String grantType;
	
	@Value("${keycloak.username}")
	private String username;
	
	@Value("${keycloak.password}")
	private String password;
	
	public Keycloak getKeycloakInstance() {
		if(keycloak == null) {
			keycloak = KeycloakBuilder
					.builder().serverUrl(serverUrl).realm(realm)
					.clientId(clientId).grantType(grantType)
					.username(username).password(password).build();
		}
		return keycloak;
	}
}
```


`SecurityConfig.java`
```java
package com.springboot.keycloak.example.app.security;


import org.springframework.context.annotation.Bean;
import org.springframework.security.config.Customizer;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.http.SessionCreationPolicy;
import org.springframework.security.web.SecurityFilterChain;

public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http)
            throws Exception {
        http.csrf(t -> t.disable());
        http.authorizeHttpRequests(
                authorize -> authorize
                        .anyRequest().authenticated()
//                t -> t
//                        .requestMatchers("/restaurants/**").hasRole("user")
//                        .requestMatchers("/menus/**").hasRole("user")
//                        .anyRequest().permitAll()
        );

        http.oauth2ResourceServer(
                t -> t.jwt(Customizer.withDefaults())
        );

        http.sessionManagement(
                t -> t.sessionCreationPolicy(SessionCreationPolicy.STATELESS)
        );
        return http.build();
    }
}

```

#### Create application properties

`application-dev.properties`
```properties
server.port=8090

spring.datasource.url=jdbc:h2:file:./data/demo
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=sa
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.h2.console.enabled=true
spring.h2.console.settings.trace=false
spring.h2.console.settings.web-allow-others=false

spring.security.oauth2.resourceserver.jwt.issuer-uri=http://localhost:8080/realms/mobile-cloud
# spring.security.oauth2.resourceserver.jwt.jwk-set-uri=http://localhost:8080/realms/mobile-cloud/protocol/openid-connect/certs

keycloak.realm=mobile-cloud
keycloak.server-url=http://localhost:8080
keycloak.client-id=admin-cli
keycloak.grant-type=password
keycloak.username=admin
keycloak.password=admin
```

`application-prod.properties`

```properties
server.port=8080

spring.datasource.url=jdbc:postgresql://localhost:5432/demo
spring.datasource.driver-class-name=org.postgresql.Driver
spring.datasource.username=your_postgres_user
spring.datasource.password=your_postgres_password
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect

spring.security.oauth2.resourceserver.jwt.issuer-uri=http://localhost:8080/realms/mobile-cloud
# spring.security.oauth2.resourceserver.jwt.jwk-set-uri=http://localhost:8080/realms/mobile-cloud/protocol/openid-connect/certs

keycloak.realm=mobile-cloud
keycloak.server-url=http://localhost:8080
keycloak.client-id=admin-cli
keycloak.grant-type=password
keycloak.username=admin
keycloak.password=admin
```

`application.properties`

```properties
spring.application.name=springboot-keycloak-app
spring.profiles.active=dev
```



`docker-compose.yml`

```docker
name: openldap
services:
  openldap:
    image: osixia/openldap:latest
    container_name: openldap
    hostname: openldap
    ports: 
      - "389:389"
      - "636:636"
    volumes:
      - ./data/certificates:/container/service/slapd/assets/certs
      - ./data/slapd/database:/var/lib/ldap
      - ./data/slapd/config:/etc/ldap/slapd.d
      # - ./ldifs/10-bootstrap.ldif:/container/service/slapd/assets/config/bootstrap/ldif/custom/10-bootstrap.ldif
    environment: 
      - LDAP_ORGANISATION=example
      - LDAP_DOMAIN=example.org
      - LDAP_ADMIN_USERNAME=admin
      - LDAP_ADMIN_PASSWORD=admin_pass
      - LDAP_CONFIG_PASSWORD=config_pass
      - "LDAP_BASE_DN=dc=example,dc=org"
      - LDAP_TLS_CRT_FILENAME=server.crt
      - LDAP_TLS_KEY_FILENAME=server.key
      - LDAP_TLS_CA_CRT_FILENAME=example.org.ca.crt
      - LDAP_READONLY_USER=true
      - LDAP_READONLY_USER_USERNAME=user-ro
      - LDAP_READONLY_USER_PASSWORD=ro_pass
    networks:
      - openldap
    depends_on:
      - postgres
      - keycloak
    restart: unless-stopped

  phpldapadmin:
    image: osixia/phpldapadmin:latest
    container_name: phpldapadmin
    hostname: phpldapadmin
    ports: 
      - "80:80"
    environment: 
      - PHPLDAPADMIN_LDAP_HOSTS=openldap
      - PHPLDAPADMIN_HTTPS=false
    depends_on:
      - openldap
    networks:
      - openldap

  postgres:
    container_name: postgres
    image: postgres
    environment:
      POSTGRES_USER: username
      POSTGRES_PASSWORD: password
      POSTGRES_DB: keycloakdb
    volumes:
      - ./postgres:/var/lib/postgresql/data
    ports:
      - 54321:5432
    networks:
      - openldap
    restart: unless-stopped

  keycloak:
    container_name: keycloak
    image: quay.io/keycloak/keycloak:24.0.2
    ports:
      - 8080:8080
    environment:
      KEYCLOAK_ADMIN: admin
      KEYCLOAK_ADMIN_PASSWORD: admin
      KC_HOSTNAME: localhost
      KC_HOSTNAME_PORT: 8080
      KC_HOSTNAME_STRICT_BACKCHANNEL: false
      KC_HTTP_ENABLED: true
      KC_HOSTNAME_STRICT_HTTPS: false
      KC_HEALTH_ENABLED: true
      KC_DB: postgres
      KC_DB_URL: jdbc:postgresql://postgres:5432/keycloakdb
      KC_DB_USERNAME: username
      KC_DB_PASSWORD: password
    depends_on:
      - postgres
    networks:
      - openldap
    command:
      - "start"
    restart: unless-stopped

networks:
  openldap:
    driver: bridge

# https://dev.to/alibenromdhan/how-to-set-up-and-configure-openldap-in-a-docker-container-with-phpldapadmin-1ido

# http://localhost
# To log in, enter cn=admin,dc=example,dc=org as the username and admin_pass as the password.
```

## 🔐 Keycloak LDAP Configuration

### General Options
- **UI Display Name**: `ldap`
- **Vendor**: `Other`

### Connection and Authentication
- **Connection URL**: `ldap://openldap:389`
- **Enable StartTLS**: `Off`
- **Bind Type**: `simple`
- **Bind DN**: `cn=admin,dc=example,dc=org`
- **Bind Credentials**: `admin_pass`

### LDAP Searching and Updating
- **Edit Mode**: `READ_ONLY`
- **Users DN**: `ou=people,dc=example,dc=org`
- **Search Scope**: `Subtree`
- **Username LDAP Attribute**: `uid`
- **RDN LDAP Attribute**: `uid`
- **UUID LDAP Attribute**: `entryUUID`
- **User Object Classes**: `inetOrgPerson, organizationalPerson`
- **User LDAP Filter**: `(objectClass=inetOrgPerson)`

### Synchronization Settings
- **Import Users**: `On`
- **Sync Registrations**: `On`
- **Periodic Full Sync**: `On`
- **Full Sync Period**: `-1`
- **Periodic Changed Users Sync**: `On`
- **Changed Users Sync Period**: `-1`

## ✅ Troubleshooting Tips
- Ensure `Users DN` matches actual LDAP structure.
- Use `phpLDAPadmin` to verify user entries and attributes.
- Check Keycloak logs for detailed error messages.

## 📎 References
- [OpenLDAP Docker Setup](https://dev.to/alibenromdhan/how-to-set-up-and-configure-openldap-in-a-docker-container-with-phpldapadmin-1ido)

#### References:
https://github.com/dive-into-dev/springboot-keycloakauth  

https://www.youtube.com/watch?v=oWUGe-Z0WF0&list=PLHXvj3cRjbzs8TaT-RX1qJYYK2MjRro-P&index=12

# CSNG (Compile Safe Name Generator)

[![Apache 2.0](https://img.shields.io/github/license/making/csng.svg)](https://www.apache.org/licenses/LICENSE-2.0) [![Maven Central](https://maven-badges.herokuapp.com/maven-central/am.ik.csng/csng/badge.svg)](https://maven-badges.herokuapp.com/maven-central/am.ik.csng/csng) [![Javadocs](https://www.javadoc.io/badge/am.ik.csng/csng.svg)](https://www.javadoc.io/doc/am.ik.csng/csng) [![Actions Status](https://github.com/making/csng/workflows/CI/badge.svg)](https://github.com/making/csng/actions)

## How to use

```xml
<dependency>
    <groupId>am.ik.csng</groupId>
    <artifactId>csng</artifactId>
    <version>0.2.0</version>
    <optional>true</optional>
</dependency>
```

## Examples

### Java Beans (Using getters)

```java
package test;

import am.ik.csng.CompileSafeName;

public class CarBean {
    private String name;
    private int gas;

    public CarBean(String name, int gas) {
        this.name = name;
        this.gas = gas;
    }

    @CompileSafeName
    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @CompileSafeName
    public int getGas() {
        return this.gas;
    }

    public void setGas(int gas) {
        this.gas = gas;
    }
}
```

generates

```java
package test;

public class _CarBeanName {
    public static final class Name {
        public static final String LOWER_CAMEL = "name";
        public static final String UPPER_CAMEL = "Name";
        public static final String LOWER_UNDERSCORE = "name";
        public static final String UPPER_UNDERSCORE = "NAME";
    }

    public static final class Gas {
        public static final String LOWER_CAMEL = "gas";
        public static final String UPPER_CAMEL = "Gas";
        public static final String LOWER_UNDERSCORE = "gas";
        public static final String UPPER_UNDERSCORE = "GAS";
    }
}
```

### Using non-getters

```java
package test;

import am.ik.csng.CompileSafeName;

public class Car {
	private final String name;
	private final int gas;

	public Car(String name, int gas) {
		this.name = name;
		this.gas = gas;
	}

	@CompileSafeName(getter = false)
	public String name() {
		return this.name;
	}

	@CompileSafeName(getter = false)
	public int gas() {
		return this.gas;
	}
}
```

generates

```java
package test;

public class _CarName {
	public static final class Name {
		public static final String LOWER_CAMEL = "name";
		public static final String UPPER_CAMEL = "Name";
		public static final String LOWER_UNDERSCORE = "name";
		public static final String UPPER_UNDERSCORE = "NAME";
	}

	public static final class Gas {
		public static final String LOWER_CAMEL = "gas";
		public static final String UPPER_CAMEL = "Gas";
		public static final String LOWER_UNDERSCORE = "gas";
		public static final String UPPER_UNDERSCORE = "GAS";
	}
}
```

### Constructor

```java
package test;

import am.ik.csng.CompileSafeProperties;

public class Car2 {
	private final String name;
	private final int gas;

	@CompileSafeProperties
	public Car2(String name, int gas) {
		this.name = name;
		this.gas = gas;
	}

	public String name() {
		return this.name;
	}

	public int gas() {
		return this.gas;
	}
}
```

generates

```java
package test;

public class _Car2Properties {
	public static final class Name {
		public static final String LOWER_CAMEL = "name";
		public static final String UPPER_CAMEL = "Name";
		public static final String LOWER_UNDERSCORE = "name";
		public static final String UPPER_UNDERSCORE = "NAME";
	}

	public static final class Gas {
		public static final String LOWER_CAMEL = "gas";
		public static final String UPPER_CAMEL = "Gas";
		public static final String LOWER_UNDERSCORE = "gas";
		public static final String UPPER_UNDERSCORE = "GAS";
	}
}
```

## Required

* Java 8+

## License

Licensed under the Apache License, Version 2.0.

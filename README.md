DynamicDiscriminatorMapBundle
=============================

DynamicDiscriminatorMapBundle simplifies the use of Doctrine Single Table and Class Table Inheritance mapping strategy in Symfony2

With this bundle you can adds dynamically all classes of a hierarchy to the options of DiscriminatorMap using a config file. This way you can apply the methodology of 'decoupling'

## Installation

### Step 1: Download DynamicDiscriminatorMapBundle using composer

Add DynamicDiscriminatorMapBundle in your composer.json:

	{
    	"require": {
        	"damianociarla/dynamic-discriminator-map-bundle": "dev-master"
    	}
	}

### Step 2: Enable the bundle

Enable the bundle in the kernel:

	<?php
	// app/AppKernel.php

	public function registerBundles()
	{
	    $bundles = array(
        	// ...
        	new DCS\DynamicDiscriminatorMapBundle\DCSDynamicDiscriminatorMapBundle(),
    	);
	}

## Configuration

### Parent class

This is an example of a parent class

	<?php
    namespace Acme\PersonBundle\Entity;

    /**
     * @ORM\Entity
     * @ORM\Table(name="person")
     * @ORM\InheritanceType("SINGLE_TABLE")
     * @ORM\DiscriminatorColumn(name="type", type="string")
     * @ORM\DiscriminatorMap({"person" = "Person"})
     */
    class Person
    {
        // ...
    }

### Children classes

This is an example of two children classes

	<?php
    namespace Acme\StudentBundle\Entity;

    use Acme\PersonBundle\Entity\Person;

    /**
     * @ORM\Entity
     */
    class Student extends Person
    {
        // ...
    }

	<?php
    namespace Acme\TeacherBundle\Entity;

    use Acme\PersonBundle\Entity\Person;

    /**
     * @ORM\Entity
     */
    class Teacher extends Person
    {
        // ...
    }

### Configuration file

    # app/config/config.yml
    dcs_dynamic_discriminator_map:
        mapping:
            person:
                entity: Acme\PersonBundle\Entity\Person
                map:
                    student: Acme\StudentBundle\Entity\Student
                    teacher: Acme\TeacherBundle\Entity\Teacher
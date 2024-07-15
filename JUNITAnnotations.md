<< [README](./README.md)

# Contents
- [Annotations](#annotations)
    - [@BeforeClass](#-beforeclass)
    - [@Before](#before)
    - [@Test](#test)
    - [@After](#after)
- [Resources]

Note that multiple methods of the same annotation type may run in any order 

## Annotations
### @ BeforeClass
BeforeClass -- Method should be run once before any of the test methods in the class e.g. Setting up a database connection 

### @Before
Before -- Method should be run before each test method e.g. Loading data from a database 

### @Test
Test -- Method is a test method Tests either pass or fail, and only fail if an unhandled exception is thrown 

### @After
After -- Method should be run after each test method e.g. Used to delete/rollback things that were setup 

### @AfterClass
AfterClass -- Method should be run once after all test methods in a class have been run e.g. Final cleanup
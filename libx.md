# Learning LibX

## ModXRegistration

When extending **ModXRegistration**, the following events are automatically registered on your **Mod ID**:

* FMLCommonSetup;
* FMLClientSetup;

```java
public final class ModClass extends ModXRegistration {
    
    public ModClass(String modId, CreativeModTab tab){
        super(modId, tab);
    }

    @Override
    protected void setup(FMLCommonSetupEvent event) {
        //NOOP
    }

    @Override
    protected void clientSetup(FMLClientSetupEvent event) {
        //NOOP
    }
}
```

### Initializing the registration.

**ModXRegistration** has an abstract method called <span style="color: #EF654E">**initRegistration(RegistrationBuilder)**</span> that is used to configure the **RegistrationBuilder**.

The **RegistrationBuilder** holds the transformers used to register your objects to Forge registering system and other transformers that you can add to implement or own objects that aren't available in the ForgeRegistries.

So everything related to the RegistrationBuilder you need to initialize it on <span style="color: #EF654E">**initRegistration(RegistrationBuilder)**</span>.

```java
    @Override
    protected void initRegistration(RegistrationBuilder builder) {
        builder.setVersion(1);
    }
```

In the example above we set the builder version to 1 because it's the current version of **LibX Registration System**.

* If you don't set the version the mod will crash.
* If you give it a version greater than then the current LibX supports the mod will crash.
* If you set the version to zero, the LibX Registration System will not be used.

You can learn more about the amazing **RegistrationBuilder** in the docs available in the class itself.

### AutoReg

**ModXRegistration** also takes care of content registration if you give it the right conditions.

**Conditions:**

* Create a class that is annotated with the **@RegisterClass** annotation.
  * All the <span style="color: #EF654E">**_public static final_**</span> objects in the annotated class will be registered with the LibX registering system.
    * ```java
      @RegisterClass
      public class ModBlocks {
         public static final BlaBlock BLA = new BlaBlock();     
      }  
      ```
  * You can also implement **Registerable** on your object to register dependencies.
    * **BlockBase** is one of the LibX base classes that implements **Registerable** and adds an Item as a dependency, this make the Registration System to register a **Block** and a **BlockItem**.  
    * See the **BlockBase** source code for more info.
* You can also create methods to register your objects and use <span style="color: #EF654E">**ModXRegistration::addRegistrationHandler(Runnable)**</span>.
  * ```java
      BlaBlock bla = null;
     
      public void initBlocks() {
         bla = new BlaBlock();     
      }
      ```
  * For simple registration you can use <span style="color: #EF654E">**ModXRegistration::register(String id, Object obj)**</span>, this will register a simple object with the defined id.
  
For more info on **ModXRegistration** check the source code.




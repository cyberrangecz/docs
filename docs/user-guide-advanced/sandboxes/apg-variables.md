APG training is conditioned by the creation of variant answers inside the sandboxes. To create variant answers, use variables in the provisioning of the sandboxes and then create the special configuration file `variables.yml` with the following structure: 

```yaml
<variable_name>:
     - type: <variable_type>
        min: <value>
        max: <value>
        length: <value>
        prohibited: [<value>,<value>,...]

```

It allows you to set the variables to random values based on the configuration of each variable. Variables are then set and used in the provisioning of the sandbox. 

## Variable Attributes

Each variable can define the various attributes. 

**Mandatory**
 
* **type**: one of the [supported variable types](#supported-variable-types).

**Optional**

* **min**: the minimum value that is possible to generate. 
* **max**: the maximum value that is possible to generate.
* **length**: length of the generated value.
* **prohibited**: list of the excluded values.

!!! info "Legend"
        :material-window-minimize:{: .icon .black } The attribute can be set but it will be ignored during value generation.
        :material-check-bold:{: .icon .green } The attribute can be set and it will have an effect during value generation. If not specified the default value is used.

|    **type**    |                               **username**                                |                               **password**                                |                  **text**                   |                                    **port**                                    |                                    **IP**                                     |
|:--------------:|:-------------------------------------------------------------------------:|:-------------------------------------------------------------------------:|:-------------------------------------------:|:------------------------------------------------------------------------------:|:-----------------------------------------------------------------------------:|
|    **min**     |                :material-window-minimize:{: .icon .black }                |                :material-window-minimize:{: .icon .black }                | :material-window-minimize:{: .icon .black } |      :material-check-bold:{: .icon .green } <br> **default:** <br> 35000       |     :material-check-bold:{: .icon .green } <br> **default:** <br> 0.0.0.0     |
|    **max**     |                :material-window-minimize:{: .icon .black }                |                :material-window-minimize:{: .icon .black }                | :material-window-minimize:{: .icon .black } | :material-check-bold:{: .icon .green } <br> **default:** <br> ***min*** + 4000 | :material-check-bold:{: .icon .green } <br> **default:** <br> 255.255.255.255 |
| **prohibited** | :material-check-bold:{: .icon .green }  <br> **default:** <br> empty list | :material-check-bold:{: .icon .green }  <br> **default:** <br> empty list | :material-window-minimize:{: .icon .black } |    :material-check-bold:{: .icon .green } <br> **default:** <br> empty list    |   :material-check-bold:{: .icon .green }  <br> **default:** <br> empty list   |
|   **length**   |     :material-check-bold:{: .icon .green }  <br> **default:** <br> 8      |    :material-check-bold:{: .icon .green }  <br> **default:** <br> None    | :material-window-minimize:{: .icon .black } |                  :material-window-minimize:{: .icon .black }                   |                  :material-window-minimize:{: .icon .black }                  |

## Supported Variable Types

* **username**: randomly chosen username.
* **password**: randomly generated characters.
* **port**: randomly generated number.
* **text**: randomly chosen sentence.


## How to Use It?
Use the variable name in the [definition of the training level](../../user-guide-basic/training-agenda/training-definition/linear-training-definition.md#i-training-level) as **Correct  Answer - Variable Name** (enable checkbox Variant Answers) instead of a static answer **Correct Answer - Static**. See also [APG in Linear Training Definition](../trainings/trainings-overview.md#automatic-generation-problem-apg-in-linear-training-definition).

## Example

```
telnet_port:
    type: port
    min: 1500
    max: 65000
    prohibited: [2323]

secret:
    type: text

username:
    type: username

encrypted_file:
    type: password
    length: 5
```

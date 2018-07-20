# Knowage-Documentation

## Structure
                                                   
Titles are underlined with a nonalphanumeric character at least as long as the text.
* `#` for parts
* `=` for chapters
* `-` for sections
* `~` for subsections
* `^` for paragraphs

### Example

```rst
Part I
########

Chapter 2
===========

Section 3
-----------
```

---

## Codes

To adding a code you need to use this syntax:

```rst
.. code-block:: Type of language
    :linenos:
    :caption: Title.
      Text of the code
```

### Example

```rst
.. code-block:: xml
    :linenos:
    :caption: Pointing at a numerical column.
    
      <COLUMNS> 
        <COLUMN field="store_id" visible="false" editable="false" /> 
```

---

## Images

There are three differents way to add an image, its depend if it is inline of the text, if it is out of the text or if it is inside a table.

1. Added an image inline:

  Insert the `|imageX|` inside the text and then recall it outside the text (anywhere in the text) whit this syntax:
  
  ```rst
  .. |imageX| image:: media/imageX.png
              :width: dimension
  ```
                   
2. Added an image oustide:

  At the point you need to insert an image use this:
  
  ```rst
  .. figure:: media/imageX.png

    Caption of the image.
  ```

3. Added an immage inside a table:

```
   +-------------------------------+-----------------------+
   |    Icon                       | Name                  |
   +===============================+=======================+
   | .. figure:: media/imageX.png  | Name ImageX           |
   |                               |                       |
   |                               |                       |
   +-------------------------------+-----------------------+
   | .. figure:: media/imageY.png  | Name ImageY           |
   |                               |                       |
   |                               |                       |
   +-------------------------------+-----------------------+
 
```

### Example

```rst
1. If your dataset is similar to another existing dataset, you can click the **Clone** icon |image16|.

    .. |image16| image:: media/image23.png
       :width: 30
   
2. In the **Detail** tab you define the Name, the Label and an optional Description of the dataset (refer to figure below). 

    .. figure:: media/image22.png

        Dataset Panel.
 
3. +-------------------------------+-----------------------+-----------------------+
   |    Icon                       | Name                  | Description           |
   +===============================+=======================+=======================+
   | .. figure:: media/image8.png  | Knowage user          | Open a hidden menu    |
   |                               |                       | with extra            |
   |                               |                       | functionalities.      |
   +-------------------------------+-----------------------+-----------------------+
   | .. figure:: media/image9.png  | Select role           | Select the            |
   |                               |                       | authentication role   |
   |                               |                       | (available if you are |
   |                               |                       | associated to more    |
   |                               |                       | than one role).       |
   +-------------------------------+-----------------------+-----------------------+
        
```

---

## Tables

There are two different way to add an image, its depend if it is inline of the text or is out of the text.

1. Added an image inline:

  Insert the `|imageX|` inside the text and then recall it outside the text (anywhere in the text) whit this syntax:
  
  ```rst
  .. |imageX| image:: media/imageX.png
              :width: dimension
  ```
                   
2. Added an image oustide:

  At the point you need to insert an image use this:
  
  ```rst
  .. figure:: media/imageX.png

    Caption of the image.
  ```

### Example

```rst
1. If your dataset is similar to another existing dataset, you can click the **Clone** icon |image16|.

    .. |image16| image:: media/image23.png
       :width: 30
   
2. In the **Detail** tab you define the Name, the Label and an optional Description of the dataset (refer to figure below). 

    .. figure:: media/image22.png

        Dataset Panel.
```

---

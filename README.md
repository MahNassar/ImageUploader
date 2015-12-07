# ImageUploader
Simple, fast and customizable PHP 7 Image Uploader

> **Important:** This is a **PHP 7** plugin and **WILL NOT** work in older verions of PHP.


### How to use

```php
$my_file = new ImageUploader($_FILES['my_file']);

$my_file->width = 200;              // In pixels
$my_file->sendTo = 'uploads/';      // Relative path
$my_file->maxSize = 5;              // In MB

$upload = $my_file->uploadImage();  // Dispatch upload action
```

#### Handling Success & Errors

```php
...
$upload = $my_file->uploadImage();  // Dispatch upload action

if ($upload->isUploaded) {
    echo $upload->fullPath; // $upload->uploadedName for only image name
} else {
    echo $upload->errorMessage; // Tells what went wrong
}
```

#### Resizing Image

If you want to resize your image proportionally all you have to do is use `width` or `height` parameters alone. If you want to resize your image without respecting image ratio, simply use `width` and `height` together:

```php
// Will Resize respecting ratio
$my_file_one = new ImageUploader($_FILES['my_file']);

$my_file_one->width = 200;
$my_file_one->sendTo = 'uploads/';

$upload = $my_file_one->uploadImage();


// Will Resize without respecting ratio
$my_file_two = new ImageUploader($_FILES['my_file']);

$my_file_two->width = 200;
$my_file_two->width = 599; // some crazy disproportional height
$my_file_two->sendTo = 'uploads/';

$upload = $my_file_two->uploadImage();
```
> **Note:** In order to use resizing features you need Imagick extension installed. Most servers have it by default, but just make sure to check yours using `phpinfo()`. 

# Upload files from your flutter app to server

This is a simple flutter project for, how to upload files from your flutter app to your backend server.

Youtube explanation video: https://youtu.be/YCNDR2sY4xI

## Server side - saveFile.php

    <?php
    error_reporting(E_ERROR | E_PARSE);

    // Response object structure
    $response = new stdClass;
    $response->status = null;
    $response->message = null;

    // Uploading file
    $destination_dir = "upload/";
    $base_filename = basename($_FILES["file"]["name"]);
    $target_file = $destination_dir . $base_filename;

    if(!$_FILES["file"]["error"])
    {
        if (move_uploaded_file($_FILES["file"]["tmp_name"], $target_file)) {        
            $response->status = true;
            $response->message = "File uploaded successfully";

        } else {

            $response->status = false;
            $response->message = "File uploading failed";
        }    
    } 
    else
    {
        $response->status = false;
        $response->message = "File uploading failed";
    }

    header('Content-Type: application/json');
    echo json_encode($response);

# Consignmentv1
php woocommerce consignment app/plugin

 Prepare Plugin Directory Structure

 woocommerce-consignment/
  ├── woocommerce-consignment.php
  ├── includes/
        └── class-consignment-handlers.php
  └── assets/
        └── css/
        └── js/
The woocommerce-consignment.php file is your main plugin file.
includes/class-consignment-handlers.php will contain your submission and payout management logic.
The assets/css/ and assets/js/ folders are where you can place any custom styles or scripts, if needed.

Create the Main Plugin File

<?php
/*
Plugin Name: WooCommerce Consignment Store
Plugin URI: https://yoursite.com
Description: A consignment plugin for WooCommerce that allows users to submit items for sale and admin to approve/reject.
Version: 1.0
Author: John Marruffo
Author URI: https://yoursite.com
Text Domain: woocommerce-consignment
License: GPL2
*/

if (!defined('ABSPATH')) {
    exit; // Exit if accessed directly
}

// Define plugin directory path
define('WC_CONSIGNMENT_PATH', plugin_dir_path(__FILE__));

// Include necessary files
require_once WC_CONSIGNMENT_PATH . 'includes/class-consignment-handlers.php';

// Initialize the plugin
function wc_consignment_init() {
    // Register shortcodes, enqueue scripts, and handle plugin initialization
    add_shortcode('additemform', 'consignment_add_item_form');
    add_shortcode('approve_items', 'approve_reject_items');
    add_shortcode('manage_payouts', 'manage_payouts');
}
add_action('init', 'wc_consignment_init');

?>


Create the Consignment Handlers File

<?php

// Form to submit items
function consignment_add_item_form() {
    ob_start();
    ?>
    <form id="add-item-form" method="post" enctype="multipart/form-data">
        <label for="item_name">Item Name:</label>
        <input type="text" id="item_name" name="item_name" required><br><br>

        <label for="item_description">Description:</label>
        <textarea id="item_description" name="item_description" required></textarea><br><br>

        <label for="item_image">Item Image:</label>
        <input type="file" id="item_image" name="item_image" required><br><br>

        <label for="item_price">Price:</label>
        <input type="number" id="item_price" name="item_price" required><br><br>

        <label for="item_category">Category:</label>
        <?php
        $categories = get_terms('product_cat', array('hide_empty' => false));
        ?>
        <select id="item_category" name="item_category" required>
            <?php foreach ($categories as $category) : ?>
                <option value="<?php echo $category->term_id; ?>"><?php echo $category->name; ?></option>
            <?php endforeach; ?>
        </select><br><br>

        <input type="submit" name="submit_item" value="Submit Item">
    </form>
    <?php
    if (isset($_POST['submit_item'])) {
        handle_item_submission();
    }
    return ob_get_clean();
}

// Handle the item submission
function handle_item_submission() {
    // Similar to previous item submission logic
}

// Approve or reject items
function approve_reject_items() {
    // Same as before
}

// Manage Payouts
function manage_payouts() {
    // Same as before
}
?>


Upload and Activate the Plugin in WordPress
Compress the Plugin Directory:

Zip the entire woocommerce-consignment folder.
The zip file should contain your woocommerce-consignment.php file, includes/ folder, and any other assets.
Upload the Plugin to Your WordPress Site:

Go to WordPress Admin > Plugins > Add New.
Click Upload Plugin and choose your zipped plugin file.
Click Install Now and then Activate the plugin.

Making the Plugin Private
To keep the plugin private (i.e., not available in the public WordPress Plugin Repository), you can distribute it manually as described above or keep it only on your site without submitting it to the repository.

If you later want to share it privately, you can:

Host it on your own server and send the plugin file directly to others.
Use GitHub or another private repository for private sharing.
 Optional: Submit to the WordPress Plugin Store
If you wish to distribute it publicly:

Go to the WordPress Plugin Directory: Submit your plugin.
Prepare Your ReadMe File: You’ll need to create a readme.txt file following WordPress guidelines.
Review Plugin Guidelines: Ensure your plugin meets all WordPress plugin guidelines.
This step is only necessary if you plan to release the plugin publicly on the WordPress Plugin Store.



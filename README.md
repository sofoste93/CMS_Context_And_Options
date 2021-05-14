# CMS_Context_And_Options
Building a CMS: Use Context and Options
>
> Public Site vs. Staff Area
----------------------------------------------------------------------------
# The public context
- Staff can edit content (CRUD)
- Public can only read content
- Staff shows all subjects and pages
- Public shows only visible subjects and pages
- Staff shows content in raw form
- Public shows content in finished form
- Staff can preview not yet visible pages
- Public cannot preview not yet visible pages

# New Functions
- find_all_visible_subjects()
- find_all_subjects() and skip not visible
- find_all_subjects($visible=false)
- find_all_subjects($options=[])

============================================================================
# Skip hidden subjects and pages
  <!--update: skip hidden subjects and pages-->
  <?php if (!$nav_subject['visible']){ continue;} // start the next loop immediately ?>
  - do the same thing for pages

============================================================================
# Use an option for conditional code
    // parse in an array of option
    function find_all_subjects($options=[]) {
        $visible = $options['visible'] ?? false; // default value will be false
        if($visible) {
            // ...
        }
    }

    $opts = ['visible' => true, 'order' => 'ascending'];
    $subjects = find_all_subjects($opts);

===========================================================================
# Insecure direct object reference (IDOR)
- "IDOR"
- Code fails to verify a user's authorization before giving access to
  a restricted resource
- Viewing something you should not be able to see
-  Ranked #4 security thread by OWASP

> Example:
    https://onlinestore.com/receipt?id=SS48923

    <?php
        $id = mysqli_real_escape_string($connection, $_GET['id'];
        // it's insecure because there's no verification
        // the user has direct access

        $sql = "SELECT * FROM orders ";
        $sql .= "WHERE invoice_id={'$id}'";
        $result = mysqli_query($connection, $sql);

    ?>
- Database data
- Files
- Directories
- Scripts
- Functions

============================================================================
# Protect page visibility
(!) check out the code update

============================================================================
# Allow HTML in dynamic content
    3 Approaches
    - Symbolic language
    - Markdown, https://daringfireball.net/projects/markdown
    - HTMLPurifier, http://htmlpurifier.org

    PHP-Tools
    - strip_tags($string, $allowable_tags='')
    - nl2br($string)  - it converts new line into br-tags

============================================================================
# Preview content

- Add preview link on /public/staff/pages/show.php
- Include URL parameter "preview=true"
- Opens /public/index.php in a new window
- When previewing, does not check for page visibility
- Will confirm user's login status later

Changes performed:
------------------
=> index.php
    // :.Preview
    $preview = false;
    if (isset($_GET['preview'])) {
        // preview should require admin to be logged in
        $preview = $_GET['preview'] == 'true' ? true : false; // ternary operator
    }
    $visible = !$preview; // to false by default - if preview=true, visible=false

Replace true by visible -
ETC..

=> show.php
    <!--New link: Preview-->
    <div class="actions">
        <a class="action"
           href="<?php echo url_for('/index.php?id' . h(u($page['id'])) . '&preview=true'); ?>"
         target="_blank">Preview</a>
    </div>
ETC:..
=>
>
> - 
> 
> -
> 




# Contribution
>
>
>  - Lynda.com
> 
>   - Kevin Skoglund (Instructor)
>
>  - Stéphane Sob Fouodji

# wordpress_refer
wp complete query refer   ->   https://developer.wordpress.org/reference/classes/wp_query/
reference site link
1)db table refer site
   ->  (breif refer)   https://deliciousbrains.com/tour-wordpress-database/ 
   ->  (table structure)  https://usersinsights.com/wordpress-user-database-tables/  
   ->  (beginers refer)  https://blogvault.net/wordpress-database-schema/   
   
2)wordpress file directories refer site
   ->  https://www.wpbeginner.com/beginners-guide/beginners-guide-to-wordpress-file-and-directory-structure/ 
   
3)file directories structure
   ->    https://developer.wordpress.org/files/2014/10/Screenshot-2019-01-23-00.20.04.png
   
4)enqueu the css&js file in wp (function.php)
   -> https://hollypryce.com/enqueue/
   
5)wordpress query post(single.php) refer
   -> https://developer.wordpress.org/reference/classes/wp_query/
   
6)single.php query view code below
   <?php get_header();?>
<?php while ( have_posts() ) : the_post(); ?>
<div class="body">
	<div class="container">
		<div class="clear"></div>
		<div class="main">
			<div class="post content">
				<h1 class="page-title"><a href="<?php the_permalink(); ?>"><?php the_title();?></a></h1>

				<div class="content">
					<?php the_content(); ?>
				</div>
			</div>
		</div>
		<div class="clear"></div>
	</div>
</div>
<?php endwhile; ?>
<?php get_footer();?>


7)    query post sample code(all post data)
      -> $args = array(
      'post_type'=> 'post',
      'orderby'    => 'ID',
      'post_status' => 'publish',
      'order'    => 'DESC',
      'posts_per_page' => -1 // this will retrive all the post that is published 
      );
      $result = new WP_Query( $args );
      if ( $result-> have_posts() ) : ?>
      <?php while ( $result->have_posts() ) : $result->the_post(); ?>
      <?php the_title(); ?>   
      <?php endwhile; ?>
      <?php endif; wp_reset_postdata(); ?>
   
   Explain: while(condition){} ->  replace   ->while(condition) :(open bracket) &  endwhile;(close Bracket)    *same as all loops
   
   
   8)   add feauture img option in custom themes->post (section)
     function mytheme_post_thumbnails() {
    add_theme_support( 'post-thumbnails' );
}
add_action( 'after_setup_theme', 'mytheme_post_thumbnails' );

9)query post refer site
	->  https://awhitepixel.com/blog/query-posts-in-wordpress/
10)categories in wp
->  https://njengah.com/display-category-name-in-wordpress/

11) wp custom post type
 -> refer site https://www.wpbeginner.com/wp-tutorials/how-to-create-custom-post-types-in-wordpress/
 ->   // Our create custom post type function(function.php)
function create_posttype() {
 
    register_post_type( 'movies',
    // CPT Options
        array(
            'labels' => array(
                'name' => __( 'Movies' ),
                'singular_name' => __( 'Movie' )
            ),
            'public' => true,
            'has_archive' => true,
            'rewrite' => array('slug' => 'movies'),
            'show_in_rest' => true,
 
        )
    );
}

//create creategory for custom post type

//CREATE A CATEGORY FOR CUSTOM POST TYPE 
register_taxonomy('taxonomy_name','movies',array('hierarchical' => true, 'label' => 'Category', 'query_var' =>'taxonomy_name' , 'rewrite' => array( 'slug' => 'taxonomy_name' )));



// Hooking up our function to theme setup
add_action( 'init', 'create_posttype' );

12) query post advance concept   get_posts();
	->	https://kinsta.com/blog/wordpress-get_posts/
13) get category
	->   <?php 
                                            $args=array(
                                                'post_type'=>'news',
                                                'taxonomy' => 'news_category'
                                            ); 
                                            $news_categories=get_categories($args);
                                            foreach($news_categories as $categry){
                                            ?>
                                            
                                               <a href="<?php echo get_category_link($categry->term_id) ?>"><h3><?php echo $categry->name; ?></h3></a>

                                            <?php
                                            }
                                            ?>
					    
					    
14) wp ajax submit
  1)	//form(frend end)
   <form action="" method="post" class="tm-contact-form">                                
                                <div class="form-group">
                                    <input type="text" id="contact_name" name="contact_name" class="form-control" placeholder="Name"  required/>
                                </div>
                                <div class="form-group">
                                    <input type="email" id="contact_email" name="contact_email" class="form-control" placeholder="Email"  required/>
                                </div>
                                <div class="form-group">
                                    <input type="text" id="contact_subject" name="contact_subject" class="form-control" placeholder="Subject"  required/>
                                </div>
                                <div class="form-group">
                                    <textarea id="contact_message" name="contact_message" class="form-control" rows="6" placeholder="Message" required></textarea>
                                </div>

                                <button type="submit" class="tm-btn">Submit</button><br><br>  
                                <span class="contact_form_error"></span>                        
                            </form> 
			    
  2)  //function.php(enque custom js file(main.js) and enque admin-ajax.php file use wp_localize_script)
        wp_enqueue_script("ajax-script",get_template_directory_uri()."/js/main.js");  //(enque custom js file(main.js)
	wp_localize_script( 'ajax-script', 'cpm_object', array('ajax_url' => admin_url( 'admin-ajax.php' ) ));  //enque admin-ajax.php and php variable assign js 
	
 3) // ajax for main.js 
   $(document).ready(function() {
    $("form").submit(function(event) {
        event.preventDefault();
        var name = $("#contact_name").val();
        var mail = $("#contact_email").val();
        var subject = $("#contact_subject").val();
        var msg = $("#contact_message").val();
        $.ajax({
                type: 'POST',
                url: cpm_object.ajax_url, //get form data to send function.php 
                data: {
                    action: 'set_form',
                    name: name,
                    mail: mail,
                    subject: subject,
                    msg: msg
                }
            })
            .done(function(data) {

                $(".contact_form_error").html("THANK YOU FOR SUBMIT").css("color", "green");
            })
            .error(function(a) {
                $(".contact_form_error").html("SOMETHING WRONG").css("color", "red");
            });
        return false;
    });
});

 4)   // THE AJAX ADD ACTIONS
add_action( 'wp_ajax_set_form', 'set_form1' );    //execute when wp logged in  //wp_ajax_set_form -> same name for action
add_action( 'wp_ajax_nopriv_set_form', 'set_form1'); //execute when logged out

function set_form1(){
	$name = $_POST['name'];
	$email = $_POST['mail'];
    $subj=$_post['subject'];
	$message = $_POST['msg'];
	$admin =get_option('admin_email');
	echo $name;
	
	
	exit(); //must for all ajax because solve 0 add ajax data
}  

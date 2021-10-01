# Snippets Wordpress

Códigos prontos para serem usados e facilitar a vida na construção de temas.

### Carregando scripts de plugins e outros

Carregando os scripts de Plugins e do Functions.php no meu tema.

```php

// Esse deve ser inserido no header.php
wp_head();

// Esse deve ser inserido no footer.php
wp_footer();

```

### Carregando arquivos externos

Carregando arquivos externos dentro do tema a função get_template_directory_uri, ou get_theme_file_uri.

```php

<img src="<?php echo get_template_directory_uri(); ?>/images/logo.png" alt="logo da empresa">

<img src="<?php echo get_theme_file_uri('images/logo.png'); ?>" alt="logo da empresa">

```

### Carregando arquivos CSS e JS

Carregando arquivos CSS e Javascript utilizando o Hook wp_enqueue_scripts, dentro do functions.php

```php

function meus_scripts(){
  // A função wp_enqueue_style carrega o CSS e a função wp_enqueue_script carrega os arquivos Javascript

  // Paramentros são: nome do estilo, caminho, array de arquivos para experar carregar, versão, true ou false para carregar no wp_footer()

 wp_enqueue_style('style-css', get_template_directory_uri() . '/css/style.css', array(),  '', false);

  wp_enqueue_script('style-css', get_template_directory_uri() . '/js/script.js', array(), '', true);
}

add_action('wp_enqueue_scripts', 'meus_scripts');

```

### Habilitando suportes do tema

Habilitando os suportes do tema como Menus, Widget, Imagem de destaque etc. Dentro do functions.php

```php
add_theme_support('menus');
add_theme_support('widgets');
add_theme_support('custom-logo');
add_theme_support('post-thumbnails');
add_theme_support('admin-bar');
add_theme_support('align-wide');
add_theme_support('automatic-feed-links');
add_theme_support('core-block-patterns');
add_theme_support('custom-background');
add_theme_support('custom-header');
add_theme_support('custom-line-height');
add_theme_support('customize-selective-refresh-widgets');
add_theme_support('custom-spacing');
add_theme_support('custom-units');
add_theme_support('dark-editor-style');
add_theme_support('disable-custom-colors');
add_theme_support('disable-custom-font-sizes');
add_theme_support('editor-color-palette');
add_theme_support('editor-gradient-presets');
add_theme_support('editor-font-sizes');
add_theme_support('editor-styles');
add_theme_support('featured-content');
add_theme_support('html5');
add_theme_support('post-formats');
add_theme_support('responsive-embeds');
add_theme_support('starter-content');
add_theme_support('title-tag');
add_theme_support('wp-block-styles');
add_theme_support('widgets-block-editor');
```

### Hooks de carregento de funções

Hooks de perfomance que pode deixar o site mais rápido. Dentro do functions.php

```php


// after_setup_theme faz com que a função seja executada após o carregamento do tema.
function meus_scripts() {
  // Criação de menus
  // Ativação de suporte de temas
  // Etc.
}
add('after_setup_theme', 'meus_scripts');

// widgets_init faz com que a função seja executada após os widgets serem carregados.
function meus_scripts_de_widgets() {
  // Registro de uma sidebar
}
add('widgets_init', 'meus_scripts_de_widgets');

```

### Criando um menu

Criando um registro de menu para exibição no painel do WordPress. Dentro do functions.php

```php

// Registrando um menu no functions.php
register_nav_menu('primary', 'Menu principal');
register_nav_menu('secundary', 'Menu Footer');

// Exibindo o menu no site
if(has_nav_menu('primary')){
  wp_nav_menu(array(
    'theme_location' => 'primary',
    'container' => 'nav',
    'container_class' => 'class1 nav-header',
    'fallback_cb' => false
  ));
}

if(has_nav_menu('secundary')){
  wp_nav_menu(array(
    'theme_location' => 'secundary',
    'container' => 'nav',
    'container_class' => 'class1 nav-footer',
    'fallback_cb' => false
  ));
}

```

### Criando um Widget

Criando um registro de Widget para exibição no painel do WordPress. Dentro do functions.php

```php

// Criando uma sidebar para o Widget
register_sidebar(array(
  'name' => 'Menu sidebar',
  'id', => 'id-unica-sidebar',
  'description' => 'Menu sidebar para o tema',
  'before_title' => '<h3 class="widget-titulo">',
  'after_title' => '</h3>',
  'before_widget' => '<sidebar id="%1$s" class="%2$s">',
  'after_widget' => '</sidebar>',
));

// Exibindo a sidebar no site usando o arquivo sidebar.php
if(is_active_sidebar('id-unica-sidebar')) {
  dynamic_sidebar('id-unica-sidebar');
}


// Depois chama o arquivo no local da site como o footer por exemplo
<?php get_sidebar(); ?>

```

### Criando um formulário de busca

Criando um formulário de busca padrão do WordPress

```php

// Criei searchform.php
<form role="search" method="GET" class="search-form" action="<?php echo esc_url(home_url('/')); ?>">
  <input type="search" name="s" value="<?php the_search_query(); ?>" />
  <button type="submit">Buscar</button>
</form>

```

### Funções úteis

São funções que serão utilizadas sempre no desenvolvimento de um tema.

```php

// Função que carrega o arquivo header.php
<?php get_header(); ?>

// Função que carrega o arquivo footer.php
<?php get_footer(); ?>

// Função para carregar classes unicas do WordPress
<body <?php body_class(); ?>>

// Função que retornar a url do site
<?php echo get_home_url(); ?>

// Função que retorna o título da página ou post
<?php the_title();?>

// Função que retorna a imagem de destaque de post ou página
<?php the_post_thumbnail(); ?>

// Função que retorna a url da imagem de destaque
<?php get_the_post_thumbnail_url(); ?>

// Função que retorna o link de um post
<?php the_permalink() ?>

// Função que retorn um resumo do post
<?php the_excerpt(); ?>

// Função que retorna conteúdo completo do post
<?php the_content(); ?>

// Função que retorna classes únicas de um post
<?php post_class(); ?>

// Função que retorna o ID de um post, na página de post
<?php get_the_ID(); ?>

// Função que importa pedaços de código
<?php get_template_part(); ?>

// Função que retorna informações sobre o site
<?php bloginfo(); ?>

// Função que retorna true caso seja a página inicial
<?php is_home(); ?>
<?php is_front_page(); ?>

// Função que retorna true caso seja uma página de categoria
<?php is_category(); ?>
<?php is_archive(); ?>

// Função que retorna true caso seja uma página única de um post ou custom post
<?php is_single(); ?>

// Função que retorn true caso seja uma página e não um post
<?php is_page(); ?>

// Função que limpa as querys após um loop
<?php wp_reset_query(); ?>
<?php wp_reset_postdata(); ?>


// Função que retorna true se o usuário estiver logado
<?php is_user_logged_in(); ?>

// Função que retorna informações do usuário logado
<?php wp_get_current_user(); ?>

```

### Personalizado o resumo

Personalizando a quantidade de texto no excerpt, dentro do functions.php

```php

// Personalizando resumo
function custom_excerpt_length( $length ) {
 return 20;

}
add_filter( 'excerpt_length', 'custom_excerpt_length');

```

### Loop padrão de postagem

Loop que percorre e exibe os posts do WordPress no site.

```php

// Verifica se existe posts
<?php if(have_posts()): ?>

  // Percorre os posts
  <?php while(have_posts()): ?>

    // Carrega o post
    <?php the_posts(); ?>

    // Verifica se o post tem imagem de destaque, se tiver, exibe ela
    <?php if(has_post_thumbnail()): ?>
      <a href="<?php the_permalink() ?>">
        <?php the_post_thumbnail('large', array('class'=>'imagem_post')); ?>
      </a>
    <?php endif; ?>

    <h2><?php the_title(); ?></h2>
    <p><?php echo get_the_date(); ?></p>
    <p>
      <a href="<?php echo get_author_posts_url( get_the_author_meta('ID') ); ?>">
        <?php the_author(); ?>
      </a>
    </p>
    <p>
      <?php the_category('-'); ?>
    </p>
    <p>
      <?php the_excerpt(); ?>
    </p>
    <p><?php comments_number('0 comentários', 'um comentário', '% comentários'); ?></p>

  <?php endwhile; ?>

<?php else: ?>

  <p>Nenhum post foi encontrado ou cadastrado</p>

<?php endif; ?>


```

### Loop que ignora o primeiro post

Loop que percorre e exibe os posts do WordPress no site.

```php
// Loop para percorrer os posts e pegar o ID do primeiro post
<?php if(have_posts()): ?>
    <?php while(have_posts()): the_post(); ?>

      // Salvando o ID do primeiro post em uma variavel
      <?php $thePostId = get_the_ID(); ?>

    <?php endwhile; ?>
    <?php wp_reset_query(); wp_reset_postdata(); ?>
<?php endif;>


// Iniciando um novo loop, porém sem exibir o primeiro post
<?php
  $args = array (
    'posts_per_page'   => '4',
    'post__not_in'		 => array($thePostId) // Ignora o post com o ID da variavel
  );
  $query = new WP_Query ( $args );
?>

// Verifica se existe posts
<?php if($query->have_posts()): ; ?>

  <?php  while($query->have_posts()) : ?>

    <?php $query->the_post(); ?>
    <?php the_post_thumbnail(); ?>
    <?php the_title(); ?>
    <a href="<?php echo get_permalink(); ?>">Ler mais</a>

  <?php endwhile; ?>

<?php else: ?>

  <p>Nenhum post foi encontrado ou cadastrado</p>

<?php endif; ?>


```

### Exibindo lista de categorias

Exibindo uma lista com as categorias cadastradas no painel do WordPress.

```php
// Pega todas as categorias e armazena em um variável
<?php $categories = get_categories(); ?>

  // Verifica se tem categorias
  <?php if($categories): ?>

      // Percorre as categorias da variavel
      <?php foreach($categories as $category): ?>

        // Retorna da categoria o link
        <a href="<?php echo get_category_link($category); ?>">

          // Retorna da categoria o nome
          <?php echo $category->name; ?>
        </a>

      <?php endforeach; ?>
  <?php endif; ?>

```

### Exibindo paginação

Exibindo uma paginação na pagina de blog.

```php

// Depois do loop

// Página anterior
<?php previous_posts_link('Voltar'); ?>

// Próxima Página
<?php next_posts_link('Avançar'); >

// Dentro da página de post single.php

// Retorna o nome do post anterior e link
<?php previous_post_link(); ?>

// Retorna o nome do próximo post e link
<?php next_post_link(); >

```

### Evitando carregamento descessários

Removendo o carregamento de arquivos descessários do Header e do Footer.

```php

// Funções para Limpar o Header
remove_action('wp_head', 'rsd_link');
remove_action('wp_head', 'wlwmanifest_link');
remove_action('wp_head', 'start_post_rel_link', 10, 0 );
remove_action('wp_head', 'adjacent_posts_rel_link_wp_head', 10, 0);
remove_action('wp_head', 'feed_links_extra', 3);
remove_action('wp_head', 'wp_generator');
remove_action('wp_head', 'print_emoji_detection_script', 7);
remove_action('admin_print_scripts', 'print_emoji_detection_script');
remove_action('wp_print_styles', 'print_emoji_styles');
remove_action('admin_print_styles', 'print_emoji_styles');

```

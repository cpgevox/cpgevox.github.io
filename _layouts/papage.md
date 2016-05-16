---
layout: default
---

<div class="row container">
  <nav class="col-sm-8 relative">
    <h1 class="vox-header vox-title">{{ page.title }}</h1>
    <nav class="vox-main" >
    {{ content }}
    </nav>
  </nav>
  <nav class="col-sm-3 col-sm-offset-1 vox-sidebar bs-docs-sidenav">
    <div class="nav sidebar-module fixed navstacked" id="toc">
    </div>
  </nav>
</div>

<script src="http://code.jquery.com/jquery-latest.js"></script>
<script src="{{ "/js/bootstrap.js" | prepend: site.baseurl }}"></script>
<script src="{{ "/js/toc.js" | prepend: site.baseurl }}"></script>
<script type="text/javascript">
$(document).ready(function() {
  $('#toc').toc({ title: '', headers: 'h1, h2' });
  $('#toc ol').addClass("nav navstacked");
  $('body').scrollspy({ target: '#toc', offset: 100 });
  $('#toc').affix({
  offset: {
    top: 0,
    bottom: function () {
      return (this.bottom = $('.vox-footer').outerHeight(true) + 30)
    }
  }
})
});
</script>
<style>
/* all links */
.bs-docs-sidenav .nav>li>a {
    /*add trasnparent border */
    border-left: 2px solid transparent;
    color: #999;
    padding: 4px 20px;
    font-size: 16px;
    font-weight: 400;
}
.bs-docs-sidenav .nav li li a {
    padding-top: 1px;
    padding-bottom: 1px;
    padding-left: 30px;
    font-size: 12px;
}
/* active & hover links */
.bs-docs-sidenav .nav>.active>a, 
.bs-docs-sidenav .nav>li>a:hover, 
.bs-docs-sidenav .nav>li>a:focus {
    color: #563d7c;                 
    text-decoration: none;          
    background-color: transparent;  
    border-left: 2px solid #563d7c; 
}

.selected { color:red; }
</style>

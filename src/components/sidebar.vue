<template>
  <div class="sidebar-main">
        <button class="btn btn-secondary" type="button" data-bs-toggle="offcanvas" data-bs-target="#offcanvasWithBothOptions" aria-controls="offcanvasWithBothOptions">Sidebar</button>

<div class="offcanvas offcanvas-start" data-bs-scroll="true" tabindex="-1" id="offcanvasWithBothOptions" aria-labelledby="offcanvasWithBothOptionsLabel">
  <div class="offcanvas-header">
    <h5 class="offcanvas-title" id="offcanvasWithBothOptionsLabel">Setting</h5>
    <button type="button" class="btn-close" data-bs-dismiss="offcanvas" aria-label="Close"></button>
  </div>
  <div class="offcanvas-body">
    <p>Try scrolling the rest of the page to see this option in action.</p>
  </div>
</div>

</div>
</template>

<script>
export default {
  //     window.addEventListener('DOMContentLoaded', event => {
  // // Toggle the side navigation
  // const sidebarToggle = document.body.querySelector('#sidebarToggle');
  // if (sidebarToggle) {
  //     // Uncomment Below to persist sidebar toggle between refreshes
  //     // if (localStorage.getItem('sb|sidebar-toggle') === 'true') {
  //     //     document.body.classList.toggle('sb-sidenav-toggled');
  //     // }
  //     sidebarToggle.addEventListener('click', event => {
  //         event.preventDefault();
  //         document.body.classList.toggle('sb-sidenav-toggled');
  //         localStorage.setItem('sb|sidebar-toggle', document.body.classList.contains('sb-sidenav-toggled'));
  //     });
  // }
  // });
};
</script>

<style lang="scss">
.sidebar-main{
    background-color: #18191a;
    // text-align: start;
}
</style>

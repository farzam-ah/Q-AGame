<template>
     <nav class="navbar navbar-expand-lg navbar-dark bg-dark shadow-3 overflow-hidden">
  <div class="container-fluid p-3 d-flex justify-content-center  ">
      <div><a class="navbar-brand " href="#">Q&A Game</a></div>
    <div>
        <ul class="navbar-nav me-auto  ">
        <li class="nav-item">
          <a class="nav-link disabled ">correct {{ correctCount }}/{{ 10 }}</a>
        </li>
      </ul>
    </div>
    
     
    
  </div>
</nav>
</template>

<script>
export default {
    props :{
        correctCount : Number,
        totalCount : Number
    }
}
</script>

<template>
  <div>
    <b-container data-aos="fade">
      <b-row>
        <b-col>
          <TaskList />
        </b-col>
      </b-row>
    </b-container>
    <b-container fluid>
      <b-row>
        <b-col>
          <p class="link">
            <a href="https://www.zurimedina.com/" target="_blank">Zuri Medina</a> &copy; 2019
          </p>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import TaskList from "./components/TaskList.vue"

export default {
  name: 'app',
  components: {
    TaskList
  }
}
</script>

<style>
body {
  background: #5c5cff;
  background: -moz-linear-gradient(
    left,
    #5c5cff 10%,
    #5e64fd 19%,
    #6d98f2 78%,
    #72acee 100%
  );
  background: -webkit-gradient(
    left top,
    right top,
    color-stop(10%, #5c5cff),
    color-stop(19%, #5e64fd),
    color-stop(78%, #6d98f2),
    color-stop(100%, #72acee)
  );
  background: -webkit-linear-gradient(
    left,
    #5c5cff 10%,
    #5e64fd 19%,
    #6d98f2 78%,
    #72acee 100%
  );
  background: -o-linear-gradient(
    left,
    #5c5cff 10%,
    #5e64fd 19%,
    #6d98f2 78%,
    #72acee 100%
  );
  background: -ms-linear-gradient(
    left,
    #5c5cff 10%,
    #5e64fd 19%,
    #6d98f2 78%,
    #72acee 100%
  );
  background: linear-gradient(
    to right,
    #5c5cff 10%,
    #5e64fd 19%,
    #6d98f2 78%,
    #72acee 100%
  );
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#5c5cff', endColorstr='#72acee', GradientType=1 );
}
.link {
  color: #fff;
}
.link a{
  color: #fff;
  
}
.link a:hover{
  color: #000;;
  text-decoration: none;
}
</style>

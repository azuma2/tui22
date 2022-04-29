<template>
 <div>
  <button v-if="status == false" type="button" @click.prevent="like" class="btn btn-outline-warning">Like</button>
   <button v-else type="button" @click.prevent="like" class="btn btn-warning">Liked</button>
 </div>
</template>


<script>
  export let name;
</script>

<style>
  h1 {
    color: red;
  }
  .shadow-4 {
    box-shadow: 2px 2px 8px 0 rgba(0, 0, 0, 0.2);
  }
  .ba {
	  border-style: solid;
	  border-width: 1px;
  }
  .br3 {
	  border-radius: .5rem;
  }
  .pa2 {
	  padding: .5rem;
  }
  .b--black-10 {
	  border-color: rgba( 0, 0, 0, .1 );
  }
</style>

<div class="ba br3 b--black-10 pa2 shadow-4">
  <h1>This is {name}!</h1>
</div>

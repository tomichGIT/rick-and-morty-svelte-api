<script>
  export let character;

  var info = JSON.stringify(character, null, 2); // spacing level = 2
</script>

<div class="character">
  <img src={character.image} alt={character.name} />
  <h2>{character.name}</h2>
  
  <textarea class="scroll" rows="10">{info}</textarea>
</div>

<style>
  .scroll {
    width:100%;
    border: 2px dotted #990000;
    color:white;
    background-color: transparent;
  }

  .scroll::-webkit-scrollbar {
   display: none;
 }
</style>
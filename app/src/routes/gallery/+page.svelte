<script lang="ts">
  import {
    Card,
    Heading,
    Hr,
    Img,
    Modal,
    P} from 'flowbite-svelte';
  import galleryJson from '$lib/assets/gallery.json';

  let modalOpen = false;
  let modalName = "";
  let modalSubmittedBy = "";
  let modalUrl = "";

  const gallery = shuffle(Object.values(galleryJson)[0] as []);

  function shuffle(galleryArray: []) {
  let currentIndex = galleryArray.length;

  // While there remain elements to shuffle...
  while (currentIndex != 0) {

    // Pick a remaining element...
    let randomIndex = Math.floor(Math.random() * currentIndex);
    currentIndex--;

    // And swap it with the current element.
    [galleryArray[currentIndex], galleryArray[randomIndex]] = [
      galleryArray[randomIndex], galleryArray[currentIndex]];
  }

  return galleryArray;
}
</script>

<div class="grid gap-6 mb-6 md:grid-cols-1 w-4/5">
    <Heading tag="h2" class="p-4">Magic Community Art Gallery</Heading>
    <P class="p-4">Showcasing user submissions of the finest MS Paint art from the Magic community. Have awesome art you want to see here? Tag me with your submission on Twitter <a href="https://twitter.com/akmindt">@akmindt</a></P>
    <Hr classHr="my-8" />

    <div class="grid gap-6 mb-6 md:grid-cols-3 w-full">
      {#each gallery as {name, submittedBy, url}}
        <Card size="lg" on:click={() => {
          modalOpen = true;
          modalName = name;
          modalSubmittedBy = submittedBy;
          modalUrl = url;
          }}>
          <div>
            <Img src={url} alt="Art by {submittedBy}" />
            <P class="p-4">{name} by <a href="https://twitter.com/{submittedBy}">{submittedBy}</a></P>
          </div>
        </Card>
        
      {/each}
      <Modal title={modalName} bind:open={modalOpen} autoclose outsideclose>
        <Img src={modalUrl} alt="Art by {modalSubmittedBy}" />
        <P class="p-4">Submitted by <a href="https://twitter.com/{modalSubmittedBy}">{modalSubmittedBy}</a></P>
      </Modal>
    </div>
</div>
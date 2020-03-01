<script>
  export let onUpload = () => {};

  let name = false;

  function onFileChange(e) {
    if (e.target.files.length) {
      const file = e.target.files[0];

      if (file.type.match("image.*")) {
        name = file.name;
        const fr = new FileReader();
        fr.onload = () => {
          onUpload(fr.result);
        };
        fr.readAsDataURL(e.target.files[0]);
      }
    }
  }
</script>

<style lang="scss">
  .file-choose {
    display: flex;

    &:hover,
    &:focus {
      opacity: 0.5;
      cursor: pointer;
    }

    span {
      white-space: pre;
      text-overflow: ellipsis;
      overflow: hidden;
    }

    input {
      display: none;
    }
  }
</style>

<label class="file-choose">
  <span>{name || 'Click to choose'}</span>
  <input on:change={onFileChange} type="file" />
</label>

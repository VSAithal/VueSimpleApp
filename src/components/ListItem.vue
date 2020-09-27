<template>
  <div>
    <input
      type="number"
      name="name"
      class="list-group-item form-control inputStyle"
      :value="item.value"
      @change="$emit('text-change', item.id)"
      @keypress="validateChars"
    />
  </div>
</template>
<script>
export default {
  name: "ListItem",
  props: ["item"],
  data() {
    return {
      name: "",
    };
  },
  methods: {
    // Validation to accept only numbers and minus
    validateChars: function(evt) {
      console.log("check");
      evt = evt ? evt : window.event;
      var charCode = evt.which ? evt.which : evt.keyCode;
      console.log(charCode);
      if (
        charCode > 31 &&
        (charCode < 48 || charCode > 57) &&
        charCode !== 46 &&
        charCode !== 45
      ) {
        evt.preventDefault();
      } else {
        return true;
      }
    },
  },
};
</script>

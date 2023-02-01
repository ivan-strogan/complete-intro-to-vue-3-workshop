<script>
export { planeList, setPlaneList };

let planeList = [
  {
    name: "F-16",
    classification: ["Fighter"],
  },
  {
    name: "Mig-29",
    classification: ["Fighter"],
  },
  {
    name: "Su-27",
    classification: ["Fighter", "Bomber"],
  },
  {
    name: "Tu-24",
    classification: ["Bomber"],
  },
  {
    name: "U-2",
    classification: ["Spy"],
  },
];
function setPlaneList(value) {
  planeList = value;
}
</script>

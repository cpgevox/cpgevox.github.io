---
layout: papage
title: Le Lycée Vaucanson
---

Oh, quel beau lycée&nbsp;!

<div class="thumbnail">
<div id="googleMap" class="img-responsive" style="height:380px;"></div>
</div>

<script src="http://maps.googleapis.com/maps/api/js"></script>
<script>
function initialize() {
    var voxPosition = new google.maps.LatLng(45.170612,5.708356);
  var mapProp = {
    center:voxPosition,
    zoom:16,
    mapTypeId:google.maps.MapTypeId.HYBRID
  };
  var map=new google.maps.Map(document.getElementById("googleMap"),mapProp);
  var marker=new google.maps.Marker({
  position:voxPosition,
  });

    marker.setMap(map);
}
google.maps.event.addDomListener(window, 'load', initialize);
</script>

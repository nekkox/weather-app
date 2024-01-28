<script setup>
    import { ref, onMounted } from "vue";
    const coords = ref();
    const geolocationBlockedByUser = ref(false);
    const getGeolocation = () => {
        return new Promise((resolve, reject)=>{
            navigator.geolocation.getCurrentPosition(
                (position)=>{
                    coords.value = {
                        latitude: position.coords.latitude,
                        longitude: position.coords.longitude
                    }
                    resolve('working');
                },
                (error)=>{
                    geolocationBlockedByUser.value = true;
                    reject(error);
                }
            );
        });
    }

    onMounted(async ()=>{
        const getLocation = await getGeolocation()
        console.log(getLocation);
    })
</script>

<template>


</template>
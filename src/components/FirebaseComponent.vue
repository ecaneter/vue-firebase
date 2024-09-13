<template>
    <div>
        <h1>Productos Chilenos</h1>
        <ul>
            <li v-for="producto in productos" :key="producto.id">
                {{ producto.nombre }}
            </li>
        </ul>
    </div>
</template>

<script>

    import { getFirestore, collection, getDocs } from "firebase/firestore";
    import firebaseApp from "../firebaseConfig";

    export default {
        name: "FirebaseComponent",
        data() {
            return {
                productos: []
            }
        },
        async mounted() {
            try {
                const db = getFirestore(firebaseApp);
                const querySnapshot = await getDocs(collection(db, "productos"));

                querySnapshot.forEach((doc) => {
                    this.productos.push(doc.data());
                });

            } catch (error) {
                console.error(error);
            }
        }
    }

</script>
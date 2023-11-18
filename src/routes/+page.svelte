
<script lang="ts">


import { initializeApp } from "firebase/app";
import { getFirestore, doc, setDoc } from "firebase/firestore";
import { docStore } from "sveltefire";

const firebaseConfig = {
    apiKey: "AIzaSyDfGfq7Gi2hAi1V8JlrFGMM3XsIdHLOqY4",
    authDomain: "palm-summarizer-be658.firebaseapp.com",
    projectId: "palm-summarizer-be658",
    storageBucket: "palm-summarizer-be658.appspot.com",
    messagingSenderId: "176707039472",
    appId: "1:176707039472:web:eff34bc9986b8c0130d235"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);

const textDoc = docStore<any>(db, "text_documents/1");

async function handleSubmit(event: SubmitEvent) {
    const data = new FormData(event.target as HTMLFormElement);

    await setDoc(textDoc.ref!, {
        text: data.get("text"),
    });
}

</script>

<h1>Palm Reader</h1>
<h2>User Input</h2>

<form on:submit|preventDefault={handleSubmit}>
    <textarea name="text" />
    <input type="submit" />
</form>

{$textDoc?.text}

<h2>Palm2 Output</h2>
{$textDoc?.summary}

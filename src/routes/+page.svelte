
<svelte:head>
    <link rel="stylesheet" href="https://unpkg.com/@picocss/pico@latest/css/pico.min.css">
</svelte:head>

<script>
    let toDoList = []
    
    let texInput = ""
    

    function addTodo(){
        toDoList = [...toDoList, {content:texInput, editing:false, checked:false}]
    }

    function setEditing(i, isEditing){
        toDoList[i].editing = isEditing
    }

    function deleteTodo(i){
        toDoList.splice(i,1)
        toDoList=toDoList
    }
</script>


    <div style="margin: 0 auto; padding: 20px; width: 700px">
        <h2 style="text-align: center;">ToDo List</h2>
        <div style="display: flex;">
            <input type="text"bind:value={texInput}>
            <button style="width: 200px;" on:click={addTodo}>Ekle</button>
        </div>

    </div>

    {#each toDoList as todo, i }
    <div style="display: flex; align-items:baseline; width:700px; margin:0 auto;">
        {#if todo.editing}
            <input type="text" bind:value={todo.content}>
        {:else}
            <h4 style="flex-grow: 1;">{todo.content}</h4>
        {/if}
        <div style="display:flex;">
            {#if todo.editing}
                <button on:click={()=>setEditing(i,false)}>Kaydet</button>
            {:else}
                <button on:click={()=>setEditing(i,true)}>Düzenle</button>
            {/if}
            <button on:click={()=> deleteTodo(i)}>Sil</button>
        </div>
    </div>
        
    {/each}



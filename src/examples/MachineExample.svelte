<script lang="ts">
    import Pre from '../components/Pre.svelte'
    import ActionBar from '../components/ActionBar.svelte'
    import { Machine, interpret, send } from 'xstate'

    let submitMachine = Machine({
        id: 'submit',
        initial: 'edit',
        states: {
            edit: {
                on: {
                    SUBMIT: 'submit'
                }
            },
            submit: {
                on: {
                    SUCCESS: 'success',
                    ERROR: 'error'
                }
            },
            error: {
                on: {
                    EDIT: 'edit'
                }
            },
            success: {
                type: 'final'
            },
        }        
    })

    let obj:any = {}
    let service = interpret(submitMachine).onTransition(t => {
        obj = t
    })
    service.start()

    function actionBarItem(e, name) {
        e.preventDefault()
        service.send(name)
    }

    
</script>

<ActionBar>
    <a href="/*" on:click={e => actionBarItem(e, 'SUBMIT')}>SUBMIT</a>
    <a href="/*" on:click={e => actionBarItem(e, 'ERROR')}>ERROR</a>
    <a href="/*" on:click={e => actionBarItem(e, 'SUCCESS')}>SUCCESS</a>
    <a href="/*" on:click={e => actionBarItem(e, 'EDIT')}>EDIT</a>
</ActionBar>

<div>
    <h2>Form</h2>
    <h3>{obj.value}</h3>
    <Pre obj={obj} />

</div>
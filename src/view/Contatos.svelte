<script>
	import { contatos, generateId, operadoras } from '../contatosStore.js';
	import { nameValidate, phoneValidate } from '../validation/inputValidation.js';
	
	let novoContato = {"id": generateId()};
	let selected;
	let contatosSelecionados = [];
	
	function addContato() {
		novoContato.operadora = selected;
		$contatos = [novoContato, ...$contatos];
		novoContato = {"id": generateId()};
		selected;
	};
	
	function excluirContato() {
		$contatos = $contatos.filter(contato => !contatosSelecionados.includes(contato));
		contatosSelecionados = [];
	};
	
</script>

<div class="
position-absolute top-50 start-50 translate-middle
shadow rounded bg-light bg-gradient text-dark 
p-3 mb-2 w-50 h-auto "
>
	<input class="form-control" type="text" placeholder="Pesquisar">
		<table class="table table-striped">
			<thead>
				<tr>
					<th></th>
					<th>Código Cliente</th>
					<th>Nome</th>
					<th>Telefone</th>
					<th>Operadora</th>
					<th>Data</th>
				</tr>
			</thead>
			<tbody>
				<tr>
					<td></td>
					<td>{novoContato.id}</td>
					<td><input bind:value={novoContato.nome} class="form-control" type="text" placeholder="Nome"></td>
					<td><input bind:value={novoContato.telefone} class="form-control" type="text" placeholder="Telefone"></td>
					<td>
						<select class="form-control" bind:value={selected}>
						{#each $operadoras as operadora}
							<option value={operadora}>{operadora.nome}</option>
						{/each}
						</select>
					</td>
					<td><input bind:value={novoContato.data} class="form-control" type="date" placeholder="Data"></td>
				</tr>
				{#each $contatos as contato(contato.id)}
				<tr>
					<td><input type="checkbox" bind:group={contatosSelecionados} value={contato} ></td>
					<td>{contato.id}</td>
					<td>{nameValidate(contato.nome)}</td>				
					<td>{phoneValidate(contato.telefone)}</td>				
					<td>{nameValidate(contato.operadora.nome)}</td>				
					<td>{contato.data}</td>				
				</tr>
				{/each}
			</tbody>
		</table>
	<div class="d-grid gap-2">
	{#if contatosSelecionados.length > 0}
		<button class="btn btn-danger" type="button" on:click="{()=> {excluirContato()}}" >Excluir Contato</button>
	{:else}
		<button class="btn btn-primary" type="button" on:click="{()=> {addContato()}}" >Criar Contato</button>
	{/if}
	</div>
</div>


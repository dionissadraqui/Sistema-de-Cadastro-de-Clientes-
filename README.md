<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pedrão Câmbio Automático - Gestão de Oficina</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Bungee&display=swap');
        
        body {
            font-family: Arial, sans-serif;
            max-width: 1100px;
            margin: 0 auto;
            padding: 20px;
            background: #000;
            color: #fff;
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(255, 0, 0, 0.1) 0%, transparent 20%),
                radial-gradient(circle at 90% 80%, rgba(255, 0, 0, 0.1) 0%, transparent 20%);
        }
        
        h1 {
            font-family: 'Bungee', cursive;
            text-align: center;
            margin: 20px 0 40px;
            font-size: 3em;
            color: #fff;
            text-shadow: 
                0 0 5px #ff0000,
                0 0 10px #ff0000,
                0 0 20px #ff0000,
                0 0 40px #ff0000,
                0 0 80px #ff0000;
            letter-spacing: 2px;
            animation: neonGlow 1.5s ease-in-out infinite alternate;
        }
        
        @keyframes neonGlow {
            from {
                text-shadow: 
                    0 0 5px #ff0000,
                    0 0 10px #ff0000,
                    0 0 20px #ff0000;
            }
            to {
                text-shadow: 
                    0 0 10px #ff0000,
                    0 0 20px #ff0000,
                    0 0 30px #ff0000,
                    0 0 40px #ff0000,
                    0 0 50px #ff0000;
            }
        }
        
        .form-container {
            background-color: rgba(30, 30, 30, 0.9);
            padding: 25px;
            border-radius: 8px;
            box-shadow: 0 0 15px rgba(255, 0, 0, 0.3);
            margin-bottom: 30px;
            border: 1px solid #ff0000;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #ff3333;
            font-size: 1.1em;
        }
        
        input, select, textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid #444;
            border-radius: 4px;
            box-sizing: border-box;
            font-size: 16px;
            background-color: #222;
            color: #fff;
            transition: all 0.3s;
        }
        
        input:focus, select:focus, textarea:focus {
            border-color: #ff0000;
            box-shadow: 0 0 8px rgba(255, 0, 0, 0.5);
            outline: none;
        }
        
        textarea {
            min-height: 120px;
            resize: vertical;
        }
        
        button {
            background: linear-gradient(to bottom, #ff0000, #990000);
            color: white;
            padding: 14px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            width: 100%;
            margin-top: 15px;
            transition: all 0.3s;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 1px;
            box-shadow: 0 4px 0 #660000;
        }
        
        button:hover {
            background: linear-gradient(to bottom, #ff3333, #cc0000);
            box-shadow: 0 4px 0 #990000;
        }
        
        button:active {
            transform: translateY(2px);
            box-shadow: 0 2px 0 #660000;
        }
        
        .error {
            color: #ff6666;
            font-size: 14px;
            margin-top: 5px;
            font-weight: bold;
        }
        
        .char-counter {
            font-size: 12px;
            color: #999;
            text-align: right;
            margin-top: 5px;
        }
        
        .char-counter.warning {
            color: #ff9900;
        }
        
        .char-counter.error {
            color: #ff3333;
        }
        
        .clientes-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 30px;
            background-color: rgba(30, 30, 30, 0.9);
            box-shadow: 0 0 15px rgba(255, 0, 0, 0.3);
            border: 1px solid #ff0000;
        }
        
        .clientes-table th, .clientes-table td {
            padding: 15px;
            text-align: left;
            border-bottom: 1px solid #444;
        }
        
        .clientes-table th {
            background: linear-gradient(to bottom, #990000, #660000);
            color: white;
            font-weight: bold;
            text-transform: uppercase;
            font-size: 0.9em;
            letter-spacing: 1px;
        }
        
        .clientes-table tr:hover {
            background-color: rgba(255, 0, 0, 0.1);
        }
        
        .actions {
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
        }
        
        .edit-btn {
            background: linear-gradient(to bottom, #2196F3, #0b7dda);
            padding: 6px 12px;
            border-radius: 3px;
            color: white;
            text-decoration: none;
            font-size: 0.9em;
            transition: all 0.2s;
        }
        
        .edit-btn:hover {
            background: linear-gradient(to bottom, #42a5f5, #1e88e5);
        }
        
        .delete-btn {
            background: linear-gradient(to bottom, #f44336, #d32f2f);
            padding: 6px 12px;
            border-radius: 3px;
            color: white;
            text-decoration: none;
            font-size: 0.9em;
            transition: all 0.2s;
        }
        
        .delete-btn:hover {
            background: linear-gradient(to bottom, #ef5350, #e53935);
        }
        
        .hidden {
            display: none;
        }
        
        .search-container {
            display: flex;
            margin-bottom: 25px;
            background-color: rgba(30, 30, 30, 0.9);
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 0 15px rgba(255, 0, 0, 0.3);
            border: 1px solid #ff0000;
        }
        
        .search-container input {
            flex: 1;
            padding: 12px;
            border: 1px solid #444;
            border-radius: 4px 0 0 4px;
            font-size: 16px;
            background-color: #222;
            color: #fff;
        }
        
        .search-container button {
            width: auto;
            padding: 12px 20px;
            border-radius: 0 4px 4px 0;
            margin: 0;
            box-shadow: none;
        }
        
        .search-icon {
            display: inline-block;
            width: 20px;
            height: 20px;
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='white'%3E%3Cpath d='M15.5 14h-.79l-.28-.27a6.5 6.5 0 0 0 1.48-5.34c-.47-2.78-2.79-5-5.59-5.34a6.505 6.505 0 0 0-7.27 7.27c.34 2.8 2.56 5.12 5.34 5.59a6.5 6.5 0 0 0 5.34-1.48l.27.28v.79l4.25 4.25c.41.41 1.08.41 1.49 0 .41-.41.41-1.08 0-1.49L15.5 14zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z'/%3E%3C/svg%3E");
            background-repeat: no-repeat;
            background-position: center;
        }
        
        .highlight {
            background-color: rgba(255, 0, 0, 0.2);
            font-weight: bold;
        }
        
        .match {
            background-color: rgba(255, 200, 0, 0.5);
            color: #ffcc00;
            font-weight: bold;
            padding: 2px;
            border-radius: 2px;
        }
        
        .modal {
            display: none;
            position: fixed;
            z-index: 1;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0,0,0,0.8);
        }
        
        .modal-content {
            background-color: #222;
            margin: 10% auto;
            padding: 25px;
            border: 1px solid #ff0000;
            width: 80%;
            max-width: 700px;
            border-radius: 8px;
            box-shadow: 0 0 20px rgba(255, 0, 0, 0.5);
            color: #fff;
        }
        
        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
            transition: color 0.3s;
        }
        
        .close:hover {
            color: #ff0000;
        }
        
        .export-buttons {
            display: flex;
            gap: 15px;
            margin: 25px 0;
            justify-content: center;
            flex-wrap: wrap;
        }
        
        .export-btn {
            background: linear-gradient(to bottom, #ff3333, #990000);
            color: white;
            padding: 12px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            transition: all 0.3s;
            font-weight: bold;
            box-shadow: 0 4px 0 #660000;
            min-width: 200px;
        }
        
        .export-btn:hover {
            background: linear-gradient(to bottom, #ff5555, #bb0000);
            box-shadow: 0 4px 0 #880000;
        }
        
        .export-btn:active {
            transform: translateY(2px);
            box-shadow: 0 2px 0 #660000;
        }
        
        .car-info {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
            padding: 20px;
            background-color: rgba(255, 0, 0, 0.1);
            border-radius: 5px;
            border: 1px dashed #ff0000;
        }
        
        .section-title {
            color: #ff3333;
            font-size: 1.2em;
            margin: 20px 0 10px;
            border-bottom: 2px solid #ff0000;
            padding-bottom: 5px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        
        .logo-container {
            text-align: center;
            margin-bottom: 20px;
        }
        
        .logo-container img {
            max-width: 200px;
            filter: drop-shadow(0 0 10px rgba(255, 0, 0, 0.7));
        }
        
        /* Responsividade */
        @media (max-width: 768px) {
            .car-info {
                grid-template-columns: 1fr;
            }
            
            h1 {
                font-size: 2em;
            }
            
            .export-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .export-btn {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="logo-container">
        <img src="https://media.giphy.com/media/H1jSPXCJmo8AZi3gdP/giphy.gif" width="150" alt="Logo Pedrão Câmbio Automático">
    </div>
    
    <h1>PEDRÃO CÂMBIO AUTOMÁTICO</h1>
    
    <div class="search-container">
        <input type="text" id="searchInput" placeholder="Pesquisar cliente, veículo, placa ou CPF...">
        <button id="searchButton"><span class="search-icon"></span> Pesquisar</button>
    </div>
    
    <div class="form-container">
        <form id="clienteForm">
            <input type="hidden" id="clienteId">
            
            <div class="section-title">Dados do Cliente</div>
            
            <div class="form-group">
                <label for="nome">Nome completo*</label>
                <input type="text" id="nome" required minlength="4" placeholder="Nome completo do cliente">
                <div id="nomeError" class="error"></div>
            </div>
            
            <div class="form-group">
                <label for="cpf">CPF*</label>
                <input type="text" id="cpf" placeholder="000.000.000-00" required>
                <div id="cpfError" class="error"></div>
            </div>
            
            <div class="form-group">
                <label for="telefone">Telefone/WhatsApp*</label>
                <input type="tel" id="telefone" placeholder="(00) 00000-0000" required>
                <div id="telefoneError" class="error"></div>
            </div>
            
            <div class="section-title">Dados do Veículo</div>
            
            <div class="car-info">
                <div class="form-group">
                    <label for="marca">Marca*</label>
                    <input type="text" id="marca" placeholder="Ex: Ford, Volkswagen..." required>
                </div>
                
                <div class="form-group">
                    <label for="modelo">Modelo*</label>
                    <input type="text" id="modelo" placeholder="Ex: Fiesta, Gol..." required>
                </div>
                
                <div class="form-group">
                    <label for="placa">Placa*</label>
                    <input type="text" id="placa" placeholder="Ex: ABC1D23" style="text-transform: uppercase" required>
                </div>
                
                <div class="form-group">
                    <label for="ano">Ano</label>
                    <input type="text" id="ano" placeholder="Ex: 2018/2019">
                </div>
            </div>
            
            <div class="section-title">Serviços</div>
            
            <div class="form-group">
                <label for="servicos">Serviços Realizados*</label>
                <textarea id="servicos" maxlength="5000" placeholder="Descreva detalhadamente os serviços realizados no veículo..." required></textarea>
                <div id="servicosCounter" class="char-counter">0/5000 caracteres</div>
                <div id="servicosError" class="error"></div>
            </div>
            
            <div class="form-group">
                <label for="valor">Valor do Serviço (R$)</label>
                <input type="number" id="valor" step="0.01" placeholder="0,00">
            </div>
            
            <button type="submit" id="submitBtn">Salvar Registro</button>
            <button type="button" id="cancelBtn" class="hidden" style="background: linear-gradient(to bottom, #f44336, #d32f2f);">Cancelar Edição</button>
        </form>
    </div>
    
    <div class="export-buttons">
        <button id="exportJson" class="export-btn">Exportar para JSON</button>
        <button id="exportCsv" class="export-btn">Exportar para Excel</button>
        <button id="importJson" class="export-btn">Importar Dados</button>
    </div>
    
    <table class="clientes-table" id="clientesTable">
        <thead>
            <tr>
                <th>Cliente</th>
                <th>Veículo</th>
                <th>Placa</th>
                <th>Contato</th>
                <th>Serviço</th>
                <th>Ações</th>
            </tr>
        </thead>
        <tbody id="clientesList">
            <!-- Registros serão adicionados aqui dinamicamente -->
        </tbody>
    </table>
    
    <!-- Modal para visualizar serviços -->
    <div id="servicosModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2 style="color: #ff3333; text-shadow: 0 0 5px rgba(255, 0, 0, 0.5);">Detalhes do Serviço</h2>
            <div id="servicosModalContent" style="white-space: pre-wrap; margin-top: 20px; line-height: 1.6;"></div>
            <div id="servicoValor" style="margin-top: 20px; font-weight: bold; color: #ffcc00;"></div>
        </div>
    </div>
    
    <!-- Modal para importar dados -->
    <div id="importModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2 style="color: #ff3333; text-shadow: 0 0 5px rgba(255, 0, 0, 0.5);">Importar Dados</h2>
            <p>Selecione um arquivo JSON para importar os registros:</p>
            <input type="file" id="fileInput" accept=".json" style="margin: 15px 0; padding: 10px; background: #333; color: #fff; border: 1px solid #444; border-radius: 4px; width: 100%;">
            <button id="confirmImport" class="export-btn" style="margin-top: 15px; width: 100%;">Importar Registros</button>
            <div id="importError" class="error" style="margin-top: 15px;"></div>
        </div>
    </div>
    
    <script>
        // Banco de dados de clientes
        let clientes = [];
        let editandoId = null;
        
        // Elementos do DOM
        const form = document.getElementById('clienteForm');
        const clientesList = document.getElementById('clientesList');
        const submitBtn = document.getElementById('submitBtn');
        const cancelBtn = document.getElementById('cancelBtn');
        const searchInput = document.getElementById('searchInput');
        const searchButton = document.getElementById('searchButton');
        const servicosInput = document.getElementById('servicos');
        const servicosCounter = document.getElementById('servicosCounter');
        const servicosModal = document.getElementById('servicosModal');
        const modalContent = document.getElementById('servicosModalContent');
        const servicoValor = document.getElementById('servicoValor');
        const closeModal = document.querySelectorAll('.close');
        const exportJsonBtn = document.getElementById('exportJson');
        const exportCsvBtn = document.getElementById('exportCsv');
        const importJsonBtn = document.getElementById('importJson');
        const importModal = document.getElementById('importModal');
        const fileInput = document.getElementById('fileInput');
        const confirmImportBtn = document.getElementById('confirmImport');
        const importError = document.getElementById('importError');
        
        // Máscara para CPF
        document.getElementById('cpf').addEventListener('input', function(e) {
            let value = e.target.value.replace(/\D/g, '');
            if (value.length > 11) value = value.substring(0, 11);
            
            if (value.length > 0) {
                value = value.replace(/(\d{3})(\d)/, '$1.$2');
                value = value.replace(/(\d{3})(\d)/, '$1.$2');
                value = value.replace(/(\d{3})(\d{1,2})$/, '$1-$2');
            }
            
            e.target.value = value;
        });
        
        // Máscara para telefone
        document.getElementById('telefone').addEventListener('input', function(e) {
            let value = e.target.value.replace(/\D/g, '');
            if (value.length > 11) value = value.substring(0, 11);
            
            if (value.length > 0) {
                value = value.replace(/^(\d{2})(\d)/g, '($1) $2');
                if (value.length > 10) {
                    value = value.replace(/(\d{5})(\d)/, '$1-$2');
                } else {
                    value = value.replace(/(\d{4})(\d)/, '$1-$2');
                }
            }
            
            e.target.value = value;
        });
        
        // Máscara para placa (formato Mercosul)
        document.getElementById('placa').addEventListener('input', function(e) {
            let value = e.target.value.toUpperCase().replace(/[^A-Z0-9]/g, '');
            if (value.length > 7) value = value.substring(0, 7);
            
            // Formatar placa no padrão Mercosul (AAA1A11) ou antigo (AAA1111)
            if (value.length > 3) {
                value = value.substring(0, 3) + '-' + value.substring(3);
            }
            
            e.target.value = value;
        });
        
        // Formatar valor monetário
        document.getElementById('valor').addEventListener('input', function(e) {
            let value = e.target.value.replace(/\D/g, '');
            value = (value/100).toFixed(2) + '';
            value = value.replace(".", ",");
            value = value.replace(/(\d)(\d{3})(\d{3}),/g, "$1.$2.$3,");
            value = value.replace(/(\d)(\d{3}),/g, "$1.$2,");
            e.target.value = value;
        });
        
        // Contador de caracteres para serviços
        servicosInput.addEventListener('input', function() {
            const length = this.value.length;
            servicosCounter.textContent = `${length}/5000 caracteres`;
            
            if (length > 4500) {
                servicosCounter.classList.add('warning');
                servicosCounter.classList.remove('error');
            } else if (length > 4900) {
                servicosCounter.classList.remove('warning');
                servicosCounter.classList.add('error');
            } else {
                servicosCounter.classList.remove('warning', 'error');
            }
        });
        
        // Função para validar CPF
        function validarCPF(cpf) {
            cpf = cpf.replace(/\D/g, '');
            
            if (cpf.length !== 11 || /^(\d)\1{10}$/.test(cpf)) {
                return false;
            }
            
            let soma = 0;
            let resto;
            
            for (let i = 1; i <= 9; i++) {
                soma += parseInt(cpf.substring(i-1, i)) * (11 - i);
            }
            
            resto = (soma * 10) % 11;
            
            if ((resto === 10) || (resto === 11)) {
                resto = 0;
            }
            
            if (resto !== parseInt(cpf.substring(9, 10))) {
                return false;
            }
            
            soma = 0;
            for (let i = 1; i <= 10; i++) {
                soma += parseInt(cpf.substring(i-1, i)) * (12 - i);
            }
            
            resto = (soma * 10) % 11;
            
            if ((resto === 10) || (resto === 11)) {
                resto = 0;
            }
            
            if (resto !== parseInt(cpf.substring(10, 11))) {
                return false;
            }
            
            return true;
        }
        
        // Função para formatar valor monetário
        function formatarValor(valor) {
            if (!valor) return 'R$ 0,00';
            return 'R$ ' + parseFloat(valor).toFixed(2).replace('.', ',').replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1.');
        }
        
        // Função para pesquisar registros
        function pesquisarClientes(termo) {
            termo = termo.trim().toLowerCase();
            
            if (termo === '') {
                renderClientes(clientes);
                return;
            }
            
            const termoNumerico = termo.replace(/\D/g, '');
            
            const resultados = clientes.map(cliente => {
                const camposEncontrados = [];
                
                if (cliente.nome.toLowerCase().includes(termo)) camposEncontrados.push('nome');
                if (cliente.cpf.replace(/\D/g, '').includes(termoNumerico)) camposEncontrados.push('cpf');
                if (cliente.telefone && cliente.telefone.replace(/\D/g, '').includes(termoNumerico)) camposEncontrados.push('telefone');
                if (cliente.servicos && cliente.servicos.toLowerCase().includes(termo)) camposEncontrados.push('servicos');
                if (cliente.marca && cliente.marca.toLowerCase().includes(termo)) camposEncontrados.push('marca');
                if (cliente.modelo && cliente.modelo.toLowerCase().includes(termo)) camposEncontrados.push('modelo');
                if (cliente.placa && cliente.placa.replace(/-/g, '').toLowerCase().includes(termoNumerico)) camposEncontrados.push('placa');
                if (cliente.ano && cliente.ano.toLowerCase().includes(termo)) camposEncontrados.push('ano');
                
                if (camposEncontrados.length > 0) {
                    return {
                        ...cliente,
                        camposEncontrados,
                        termoEncontrado: termo
                    };
                }
                
                return null;
            }).filter(cliente => cliente !== null);
            
            renderClientes(resultados);
        }
        
        // Eventos de pesquisa
        searchButton.addEventListener('click', () => pesquisarClientes(searchInput.value));
        searchInput.addEventListener('keypress', (e) => e.key === 'Enter' && pesquisarClientes(searchInput.value));
        searchInput.addEventListener('input', () => pesquisarClientes(searchInput.value));
        
        // Evento de submit do formulário
        form.addEventListener('submit', function(e) {
            e.preventDefault();
            
            document.querySelectorAll('.error').forEach(el => el.textContent = '');
            
            const cliente = {
                id: editandoId || Date.now().toString(),
                nome: document.getElementById('nome').value.trim(),
                cpf: document.getElementById('cpf').value,
                telefone: document.getElementById('telefone').value.trim(),
                marca: document.getElementById('marca').value.trim(),
                modelo: document.getElementById('modelo').value.trim(),
                placa: document.getElementById('placa').value.trim().toUpperCase(),
                ano: document.getElementById('ano').value.trim(),
                servicos: document.getElementById('servicos').value.trim(),
                valor: document.getElementById('valor').value.replace(/\D/g, '') || '0'
            };
            
            let isValid = true;
            
            // Validações
            if (cliente.nome.length < 4) {
                document.getElementById('nomeError').textContent = 'Nome deve ter pelo menos 4 caracteres!';
                isValid = false;
            }
            
            if (!validarCPF(cliente.cpf)) {
                document.getElementById('cpfError').textContent = 'CPF inválido!';
                isValid = false;
            }
            
            if (cliente.telefone.replace(/\D/g, '').length < 10) {
                document.getElementById('telefoneError').textContent = 'Telefone inválido!';
                isValid = false;
            }
            
            if (!cliente.marca) {
                document.getElementById('marca').style.borderColor = '#ff3333';
                isValid = false;
            }
            
            if (!cliente.modelo) {
                document.getElementById('modelo').style.borderColor = '#ff3333';
                isValid = false;
            }
            
            if (!cliente.placa || cliente.placa.replace(/-/g, '').length < 7) {
                document.getElementById('placa').style.borderColor = '#ff3333';
                isValid = false;
            }
            
            if (!cliente.servicos) {
                document.getElementById('servicosError').textContent = 'Descreva os serviços realizados!';
                isValid = false;
            }
            
            if (isValid) {
                if (editandoId) {
                    const index = clientes.findIndex(c => c.id === editandoId);
                    if (index !== -1) clientes[index] = cliente;
                } else {
                    const cpfExistente = clientes.some(c => c.cpf.replace(/\D/g, '') === cliente.cpf.replace(/\D/g, ''));
                    if (cpfExistente) {
                        document.getElementById('cpfError').textContent = 'CPF já cadastrado!';
                        return;
                    }
                    clientes.push(cliente);
                }
                
                renderClientes(clientes);
                form.reset();
                editandoId = null;
                submitBtn.textContent = 'Salvar Registro';
                cancelBtn.classList.add('hidden');
                searchInput.value = '';
                servicosCounter.textContent = '0/5000 caracteres';
                servicosCounter.classList.remove('warning', 'error');
            }
        });
        
        // Cancelar edição
        cancelBtn.addEventListener('click', function() {
            form.reset();
            editandoId = null;
            submitBtn.textContent = 'Salvar Registro';
            cancelBtn.classList.add('hidden');
            servicosCounter.textContent = '0/5000 caracteres';
            servicosCounter.classList.remove('warning', 'error');
        });
        
        // Modal functions
        closeModal.forEach(btn => {
            btn.addEventListener('click', function() {
                servicosModal.style.display = 'none';
                importModal.style.display = 'none';
            });
        });
        
        window.addEventListener('click', function(event) {
            if (event.target === servicosModal || event.target === importModal) {
                servicosModal.style.display = 'none';
                importModal.style.display = 'none';
            }
        });
        
        // Função para visualizar serviços
        function visualizarServicos(servicos, valor) {
            modalContent.textContent = servicos || 'Nenhum serviço registrado.';
            servicoValor.textContent = valor ? `Valor: ${formatarValor(valor)}` : '';
            servicosModal.style.display = 'block';
        }
        
        // Função para renderizar a lista de clientes
        function renderClientes(listaClientes = clientes) {
            clientesList.innerHTML = '';
            
            if (listaClientes.length === 0) {
                const row = document.createElement('tr');
                row.innerHTML = `<td colspan="6" style="text-align: center;">Nenhum registro encontrado</td>`;
                clientesList.appendChild(row);
                return;
            }
            
            listaClientes.forEach(cliente => {
                const row = document.createElement('tr');
                
                if (cliente.camposEncontrados) {
                    row.classList.add('highlight');
                }
                
                let nomeDisplay = cliente.nome;
                let marcaModelo = `${cliente.marca || '--'} ${cliente.modelo || ''}`.trim();
                let placaDisplay = cliente.placa || '--';
                let servicosResumo = cliente.servicos ? 
                    (cliente.servicos.length > 50 ? cliente.servicos.substring(0, 50) + '...' : cliente.servicos) : 
                    '--';
                
                if (cliente.camposEncontrados) {
                    if (cliente.camposEncontrados.includes('nome')) {
                        nomeDisplay = highlightText(cliente.nome, cliente.termoEncontrado);
                    }
                    if (cliente.camposEncontrados.includes('marca') || cliente.camposEncontrados.includes('modelo')) {
                        marcaModelo = highlightText(`${cliente.marca || '--'} ${cliente.modelo || ''}`.trim(), cliente.termoEncontrado);
                    }
                    if (cliente.camposEncontrados.includes('placa')) {
                        placaDisplay = highlightText(cliente.placa || '--', cliente.termoEncontrado);
                    }
                    if (cliente.camposEncontrados.includes('servicos')) {
                        servicosResumo = highlightText(servicosResumo, cliente.termoEncontrado);
                    }
                }
                
                const servicosBtn = cliente.servicos ? 
                    `<a href="#" class="edit-btn ver-servicos-btn" data-servicos="${cliente.servicos}" data-valor="${cliente.valor}">Detalhes</a>` : 
                    '--';
                
                row.innerHTML = `
                    <td>${nomeDisplay}</td>
                    <td>${marcaModelo} ${cliente.ano ? '(' + cliente.ano + ')' : ''}</td>
                    <td>${placaDisplay}</td>
                    <td>${cliente.telefone || '--'}</td>
                    <td>${servicosResumo}</td>
                    <td class="actions">
                        <a href="#" class="edit-btn" data-id="${cliente.id}">Editar</a>
                        <a href="#" class="delete-btn" data-id="${cliente.id}">Excluir</a>
                        ${servicosBtn}
                    </td>
                `;
                
                clientesList.appendChild(row);
            });
            
            // Adicionar eventos aos botões
            document.querySelectorAll('.edit-btn:not(.ver-servicos-btn)').forEach(btn => {
                btn.addEventListener('click', function(e) {
                    e.preventDefault();
                    editarCliente(this.getAttribute('data-id'));
                });
            });
            
            document.querySelectorAll('.delete-btn').forEach(btn => {
                btn.addEventListener('click', function(e) {
                    e.preventDefault();
                    if (confirm('Tem certeza que deseja excluir este registro?')) {
                        excluirCliente(this.getAttribute('data-id'));
                    }
                });
            });
            
            document.querySelectorAll('.ver-servicos-btn').forEach(btn => {
                btn.addEventListener('click', function(e) {
                    e.preventDefault();
                    visualizarServicos(
                        this.getAttribute('data-servicos'),
                        this.getAttribute('data-valor')
                    );
                });
            });
        }
        
        // Função para editar cliente
        function editarCliente(id) {
            const cliente = clientes.find(c => c.id === id);
            if (cliente) {
                document.getElementById('clienteId').value = cliente.id;
                document.getElementById('nome').value = cliente.nome;
                document.getElementById('cpf').value = cliente.cpf;
                document.getElementById('telefone').value = cliente.telefone || '';
                document.getElementById('marca').value = cliente.marca || '';
                document.getElementById('modelo').value = cliente.modelo || '';
                document.getElementById('placa').value = cliente.placa || '';
                document.getElementById('ano').value = cliente.ano || '';
                document.getElementById('servicos').value = cliente.servicos || '';
                document.getElementById('valor').value = cliente.valor ? 
                    parseFloat(cliente.valor/100).toFixed(2).replace('.', ',') : '';
                
                // Atualizar contador de caracteres
                const length = cliente.servicos ? cliente.servicos.length : 0;
                servicosCounter.textContent = `${length}/5000 caracteres`;
                if (length > 4500) servicosCounter.classList.add('warning');
                if (length > 4900) servicosCounter.classList.add('error');
                
                editandoId = id;
                submitBtn.textContent = 'Atualizar Registro';
                cancelBtn.classList.remove('hidden');
                
                form.scrollIntoView({ behavior: 'smooth' });
            }
        }
        
        // Função para excluir cliente
        function excluirCliente(id) {
            clientes = clientes.filter(c => c.id !== id);
            renderClientes(clientes);
            searchInput.value = '';
        }
        
        // Função para exportar para JSON
        function exportToJson() {
            const dataStr = JSON.stringify(clientes, null, 2);
            const dataUri = 'data:application/json;charset=utf-8,'+ encodeURIComponent(dataStr);
            
            const linkElement = document.createElement('a');
            linkElement.setAttribute('href', dataUri);
            linkElement.setAttribute('download', `pedrao_cambio_${new Date().toISOString().split('T')[0]}.json`);
            linkElement.click();
        }
        
        // Função para exportar para CSV
        function exportToCsv() {
            const headers = ['Nome', 'CPF', 'Telefone', 'Marca', 'Modelo', 'Ano', 'Placa', 'Serviços', 'Valor'];
            
            let csv = headers.join(';') + '\n';
            
            clientes.forEach(cliente => {
                const row = [
                    `"${cliente.nome}"`,
                    `"${cliente.cpf}"`,
                    `"${cliente.telefone || ''}"`,
                    `"${cliente.marca || ''}"`,
                    `"${cliente.modelo || ''}"`,
                    `"${cliente.ano || ''}"`,
                    `"${cliente.placa || ''}"`,
                    `"${(cliente.servicos || '').replace(/"/g, '""')}"`,
                    `"${cliente.valor || '0'}"`
                ];
                
                csv += row.join(';') + '\n';
            });
            
            const dataUri = 'data:text/csv;charset=utf-8,' + encodeURIComponent(csv);
            const exportFileDefaultName = `pedrao_cambio_${new Date().toISOString().split('T')[0]}.csv`;
            
            const linkElement = document.createElement('a');
            linkElement.setAttribute('href', dataUri);
            linkElement.setAttribute('download', exportFileDefaultName);
            linkElement.click();
        }
        
        // Função para importar de JSON
        function importFromJson() {
            importModal.style.display = 'block';
            importError.textContent = '';
            fileInput.value = '';
        }
        
        // Eventos dos botões de exportação/importação
        exportJsonBtn.addEventListener('click', exportToJson);
        exportCsvBtn.addEventListener('click', exportToCsv);
        importJsonBtn.addEventListener('click', importFromJson);
        
        // Evento para confirmar importação
        confirmImportBtn.addEventListener('click', function() {
            const file = fileInput.files[0];
            if (!file) {
                importError.textContent = 'Por favor, selecione um arquivo.';
                return;
            }
            
            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const importedData = JSON.parse(e.target.result);
                    
                    if (!Array.isArray(importedData)) {
                        importError.textContent = 'O arquivo deve conter um array de registros.';
                        return;
                    }
                    
                    const isValid = importedData.every(item => 
                        item.nome && item.cpf && item.telefone && item.marca && item.modelo && item.placa && item.servicos
                    );
                    
                    if (!isValid) {
                        importError.textContent = 'O arquivo não contém dados válidos da oficina.';
                        return;
                    }
                    
                    const cpfsExistentes = clientes.map(c => c.cpf.replace(/\D/g, ''));
                    const cpfsImportados = importedData.map(c => c.cpf.replace(/\D/g, ''));
                    
                    const duplicados = cpfsImportados.filter(cpf => cpfsExistentes.includes(cpf));
                    
                    if (duplicados.length > 0) {
                        if (!confirm(`Atenção: ${duplicados.length} registro(s) com CPF já existente serão sobrescritos. Deseja continuar?`)) {
                            return;
                        }
                        
                        clientes = clientes.filter(c => !duplicados.includes(c.cpf.replace(/\D/g, '')));
                    }
                    
                    clientes = [...clientes, ...importedData];
                    renderClientes(clientes);
                    importModal.style.display = 'none';
                    
                    alert(`${importedData.length} registro(s) importados com sucesso!`);
                } catch (error) {
                    importError.textContent = 'Erro ao ler o arquivo. Certifique-se de que é um JSON válido.';
                    console.error(error);
                }
            };
            reader.onerror = function() {
                importError.textContent = 'Erro ao ler o arquivo.';
            };
            reader.readAsText(file);
        });
        
        // Inicializar a lista de clientes
        renderClientes();
    </script>
</body>
</html>

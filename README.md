public class Cliente {
    private int id;
    private String nome;
    private String email;
    
}

public class ClienteFactory {
    public Cliente criarCliente(String nome, String email) {
        Cliente cliente = new Cliente();
        cliente.setNome(nome);
        cliente.setEmail(email);
        
        return cliente;
    }
}

public class ClienteDAO {
    
}

import java.sql.PreparedStatement;
import java.sql.SQLException;

public class ClienteMapper {
    public void mapToPreparedStatement(Cliente cliente, PreparedStatement preparedStatement) throws SQLException {
        preparedStatement.setString(1, cliente.getNome());
        preparedStatement.setString(2, cliente.getEmail());
        
    }
}

public class Main {
    public static void main(String[] args) {
        ClienteFactory clienteFactory = new ClienteFactory();
        ClienteDAO clienteDAO = new ClienteDAO();
        
        
        Cliente novoCliente = clienteFactory.criarCliente("João", "joao@email.com");
        clienteDAO.inserirCliente(novoCliente); 

        
        Cliente clienteRecuperado = clienteDAO.recuperarClientePorID(1); 

        
        clienteRecuperado.setNome("Novo Nome");
        clienteDAO.atualizarCliente(clienteRecuperado);

        
        clienteDAO.deletarCliente(1); 
    }
}

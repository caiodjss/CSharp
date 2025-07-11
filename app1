using System;
using System.Collections.Generic;
using System.Linq;

namespace TaskManagerApp
{
    public class Tarefa
    {
        public int Id { get; set; }
        public string Titulo { get; set; }
        public string Descricao { get; set; }
        public bool Concluida { get; set; }
    }

    public class TaskManager
    {
        private List<Tarefa> tarefas = new List<Tarefa>();
        private int idAtual = 1;

        public void AdicionarTarefa(string titulo, string descricao)
        {
            tarefas.Add(new Tarefa
            {
                Id = idAtual++,
                Titulo = titulo,
                Descricao = descricao,
                Concluida = false
            });
        }

        public void ListarTarefas()
        {
            Console.WriteLine("\n--- Lista de Tarefas ---");
            foreach (var t in tarefas)
            {
                Console.WriteLine($"ID: {t.Id}, Título: {t.Titulo}, Concluída: {(t.Concluida ? "Sim" : "Não")}");
            }
        }

        public void MarcarComoConcluida(int id)
        {
            var tarefa = tarefas.FirstOrDefault(t => t.Id == id);
            if (tarefa != null)
            {
                tarefa.Concluida = true;
                Console.WriteLine("Tarefa marcada como concluída.");
            }
            else
            {
                Console.WriteLine("Tarefa não encontrada.");
            }
        }

        public void RemoverTarefa(int id)
        {
            var tarefa = tarefas.FirstOrDefault(t => t.Id == id);
            if (tarefa != null)
            {
                tarefas.Remove(tarefa);
                Console.WriteLine("Tarefa removida.");
            }
            else
            {
                Console.WriteLine("Tarefa não encontrada.");
            }
        }
    }

    class Program
    {
        static void Main()
        {
            var taskManager = new TaskManager();
            bool continuar = true;

            while (continuar)
            {
                Console.WriteLine("\n1 - Adicionar Tarefa\n2 - Listar Tarefas\n3 - Concluir Tarefa\n4 - Remover Tarefa\n0 - Sair");
                Console.Write("Escolha uma opção: ");
                string opcao = Console.ReadLine();

                switch (opcao)
                {
                    case "1":
                        Console.Write("Título: ");
                        string titulo = Console.ReadLine();
                        Console.Write("Descrição: ");
                        string desc = Console.ReadLine();
                        taskManager.AdicionarTarefa(titulo, desc);
                        break;
                    case "2":
                        taskManager.ListarTarefas();
                        break;
                    case "3":
                        Console.Write("ID da tarefa: ");
                        if (int.TryParse(Console.ReadLine(), out int idConcluir))
                            taskManager.MarcarComoConcluida(idConcluir);
                        break;
                    case "4":
                        Console.Write("ID da tarefa: ");
                        if (int.TryParse(Console.ReadLine(), out int idRemover))
                            taskManager.RemoverTarefa(idRemover);
                        break;
                    case "0":
                        continuar = false;
                        break;
                    default:
                        Console.WriteLine("Opção inválida.");
                        break;
                }
            }
        }
    }
}

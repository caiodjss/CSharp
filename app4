using System;
using System.Collections.Generic;
using System.Linq;

namespace AgendamentoExames
{
    class Program
    {
        const int MaxPacientes = 100;
        const int MaxExames = 50;
        const int DiasJunho = 36;
        const int HorariosDia = 7;
        const int DiasSemana = 7;

        static bool[,] horariosDisponiveis = new bool[DiasJunho, HorariosDia];

        static List<Paciente> pacientes = new List<Paciente>();

        static List<Exame> exames = new List<Exame>
        {
            new Exame("Hemograma", 50.00f, 2),
            new Exame("Colesterol", 40.00f, 1),
            new Exame("Glicemia", 30.00f, 1),
            new Exame("TSH", 45.00f, 3),
            new Exame("T4L", 50.00f, 3),
            new Exame("T3T", 55.00f, 3),
            new Exame("PCR", 40.00f, 1),
            new Exame("Acido Urico", 35.00f, 1),
            new Exame("Creatinina", 30.00f, 1),
            new Exame("Ureia", 25.00f, 1),
            new Exame("B9", 50.00f, 3),
            new Exame("B12", 55.00f, 3),
            new Exame("Ferritina", 60.00f, 3),
            new Exame("PSA", 65.00f, 3),
            new Exame("TGO", 40.00f, 1),
            new Exame("TGP", 40.00f, 1),
            new Exame("FA", 35.00f, 1),
            new Exame("Bilirrubinas", 30.00f, 1),
            new Exame("Amilase", 45.00f, 2),
            new Exame("Lipase", 50.00f, 2),
            new Exame("Cloro", 25.00f, 1),
            new Exame("Sodio", 30.00f, 1),
            new Exame("Potassio", 35.00f, 1),
            new Exame("Calcio", 40.00f, 1),
            new Exame("Magnesio", 45.00f, 2),
            new Exame("Fosforo", 30.00f, 1),
            new Exame("CKMB", 55.00f, 3),
            new Exame("TP", 35.00f, 1),
            new Exame("TTPA", 40.00f, 1),
            new Exame("HG", 45.00f, 2),
            new Exame("EAS", 30.00f, 1),
            new Exame("Parasitologico", 25.00f, 1),
            new Exame("Beta-hCG", 30.00f, 1),
            new Exame("HIV", 40.00f, 1),
            new Exame("HBSAG", 45.00f, 1),
            new Exame("Anti HCV", 50.00f, 1),
            new Exame("VDRL", 35.00f, 1),
            new Exame("Rubeola", 35.00f, 1),
            new Exame("Toxo", 40.00f, 1),
            new Exame("CMV", 45.00f, 1),
            new Exame("Herpes", 50.00f, 1),
            new Exame("Dengue", 55.00f, 1),
            new Exame("Zika", 60.00f, 1),
            new Exame("Chikungunya", 65.00f, 1)
        };

        static void Main(string[] args)
        {
            // Inicializa horários
            for (int i = 0; i < DiasJunho; i++)
                for (int j = 0; j < HorariosDia; j++)
                    horariosDisponiveis[i, j] = true;

            Menu();
        }

        static void Menu()
        {
            while (true)
            {
                Console.WriteLine("\nSeja bem-vindo(a) ao CdA - Canal de Agendamentos. Digite o número correspondente.\n");
                Console.WriteLine("1 - Cadastrar novo paciente.");
                Console.WriteLine("2 - Localizar paciente.");
                Console.WriteLine("3 - Editar paciente.");
                Console.WriteLine("4 - Ver agendamentos de um dia.");
                Console.WriteLine("5 - Sair.");
                Console.Write("\nOpção: ");

                if (!int.TryParse(Console.ReadLine(), out int opcao))
                {
                    Console.WriteLine("Opção inválida.");
                    continue;
                }

                Console.Clear();

                switch (opcao)
                {
                    case 1:
                        CadastrarPaciente();
                        break;
                    case 2:
                        LocalizarPaciente();
                        break;
                    case 3:
                        EditarPaciente();
                        break;
                    case 4:
                        VerificarAgendamentosDia();
                        break;
                    case 5:
                        return;
                    default:
                        Console.WriteLine("Opção inválida.");
                        break;
                }
            }
        }

        static void CadastrarPaciente()
        {
            if (pacientes.Count >= MaxPacientes)
            {
                Console.WriteLine("Limite de pacientes atingido.");
                return;
            }

            var paciente = new Paciente();

            Console.Write("Nome Completo: ");
            paciente.NomeCompleto = Console.ReadLine();

            Console.Write("CPF: ");
            paciente.CPF = Console.ReadLine();

            Console.Write("Data Nascimento: ");
            paciente.DataNascimento = Console.ReadLine();

            Console.Write("Telefone: ");
            paciente.Telefone = Console.ReadLine();

            Console.Write("Email: ");
            paciente.Email = Console.ReadLine();

            Console.Write("Endereço: ");
            paciente.Endereco = Console.ReadLine();

            Console.Clear();

            Console.WriteLine("Deseja agendar exames? (s/n)");
            string resp = Console.ReadLine().ToLower();

            if (resp == "s")
            {
                Console.WriteLine("Exames disponíveis:");
                foreach (var exame in exames)
                    Console.WriteLine($"- {exame.Nome}");

                Console.Write("Digite os exames separados por vírgula: ");
                string entrada = Console.ReadLine();

                var nomesExames = entrada.Split(',', StringSplitOptions.RemoveEmptyEntries).Select(e => e.Trim()).ToList();

                foreach (var nome in nomesExames)
                {
                    var exame = exames.FirstOrDefault(e => e.Nome.Equals(nome, StringComparison.OrdinalIgnoreCase));
                    if (exame != null)
                    {
                        paciente.ExamesAgendados.Add(exame);
                    }
                    else
                    {
                        Console.WriteLine($"Exame inválido: {nome}");
                    }
                }

                Console.Write("Escolha o dia do agendamento (1-30): ");
                if (int.TryParse(Console.ReadLine(), out int dia) && dia >= 1 && dia <= DiasJunho - 6)
                {
                    MostrarHorarios(dia);
                    Console.Write("Escolha o horário (1-7): ");
                    if (int.TryParse(Console.ReadLine(), out int horario) &&
                        horario >= 1 && horario <= HorariosDia)
                    {
                        if (horariosDisponiveis[dia - 1, horario - 1])
                        {
                            horariosDisponiveis[dia - 1, horario - 1] = false;
                            paciente.Visita = $"Visita agendada para o dia {dia} de Junho, das {6 + horario - 1}:00 às {7 + horario - 1}:00.";
                            Console.WriteLine(paciente.Visita);
                        }
                        else
                        {
                            Console.WriteLine("Horário indisponível.");
                        }
                    }
                }
            }

            pacientes.Add(paciente);
            Console.WriteLine("Paciente cadastrado com sucesso!");
        }

        static void MostrarHorarios(int dia)
        {
            Console.WriteLine($"\nHorários disponíveis para dia {dia} de Junho:");
            for (int i = 0; i < HorariosDia; i++)
            {
                Console.ForegroundColor = horariosDisponiveis[dia - 1, i] ? ConsoleColor.Green : ConsoleColor.Red;
                Console.WriteLine($"{i + 1} - {6 + i}:00 às {7 + i}:00");
            }
            Console.ResetColor();
        }

        static void LocalizarPaciente()
        {
            Console.WriteLine("Buscar por: 1 - Nome, 2 - CPF");
            if (!int.TryParse(Console.ReadLine(), out int op))
                return;

            Console.Write("Digite o valor de busca: ");
            string valor = Console.ReadLine();

            var paciente = (op == 1)
                ? pacientes.FirstOrDefault(p => p.NomeCompleto.Equals(valor, StringComparison.OrdinalIgnoreCase))
                : pacientes.FirstOrDefault(p => p.CPF == valor);

            if (paciente != null)
            {
                ExibirPaciente(paciente);
            }
            else
            {
                Console.WriteLine("Paciente não encontrado.");
            }
        }

        static void ExibirPaciente(Paciente paciente)
        {
            Console.WriteLine($"\nNome: {paciente.NomeCompleto}");
            Console.WriteLine($"CPF: {paciente.CPF}");
            Console.WriteLine($"Telefone: {paciente.Telefone}");
            Console.WriteLine($"Email: {paciente.Email}");
            Console.WriteLine($"Endereço: {paciente.Endereco}");
            Console.WriteLine(paciente.Visita);

            float total = paciente.ExamesAgendados.Sum(e => e.Valor);
            int prazo = paciente.ExamesAgendados.Any() ? paciente.ExamesAgendados.Max(e => e.Prazo) : 0;

            if (paciente.ExamesAgendados.Any())
            {
                Console.WriteLine("\nExames Agendados:");
                foreach (var exame in paciente.ExamesAgendados)
                {
                    Console.WriteLine($"- {exame.Nome}, R$ {exame.Valor:F2}, Prazo: {exame.Prazo} dias");
                }
                Console.WriteLine($"Total: R$ {total:F2}");
                Console.WriteLine($"Prazo máximo: {prazo} dias");
            }
            else
            {
                Console.WriteLine("Nenhum exame agendado.");
            }
        }

        static void EditarPaciente()
        {
            Console.WriteLine("Buscar paciente para edição.");
            Console.Write("Digite CPF ou Nome: ");
            string busca = Console.ReadLine();

            var paciente = pacientes.FirstOrDefault(p =>
                p.CPF.Equals(busca, StringComparison.OrdinalIgnoreCase) ||
                p.NomeCompleto.Equals(busca, StringComparison.OrdinalIgnoreCase));

            if (paciente == null)
            {
                Console.WriteLine("Paciente não encontrado.");
                return;
            }

            ExibirPaciente(paciente);

            Console.WriteLine("\nDeseja adicionar novos exames? (s/n)");
            if (Console.ReadLine().ToLower() == "s")
            {
                Console.WriteLine("Exames disponíveis:");
                foreach (var exame in exames)
                    Console.WriteLine($"- {exame.Nome}");

                Console.Write("Digite exames separados por vírgula: ");
                string entrada = Console.ReadLine();
                var novos = entrada.Split(',', StringSplitOptions.RemoveEmptyEntries).Select(e => e.Trim());

                foreach (var nome in novos)
                {
                    var exame = exames.FirstOrDefault(e => e.Nome.Equals(nome, StringComparison.OrdinalIgnoreCase));
                    if (exame != null)
                    {
                        paciente.ExamesAgendados.Add(exame);
                    }
                    else
                    {
                        Console.WriteLine($"Exame inválido: {nome}");
                    }
                }
                Console.WriteLine("Exames adicionados.");
            }
        }

        static void VerificarAgendamentosDia()
        {
            Console.Write("Digite o dia (1-30): ");
            if (!int.TryParse(Console.ReadLine(), out int dia))
                return;

            var agendados = pacientes.Where(p => p.Visita != null && p.Visita.Contains($"dia {dia} de Junho")).ToList();

            if (!agendados.Any())
            {
                Console.WriteLine("Nenhum agendamento para esse dia.");
                return;
            }

            foreach (var p in agendados)
            {
                ExibirPaciente(p);
                Console.WriteLine("-------------------------------------");
            }
        }
    }

    public class Paciente
    {
        public string NomeCompleto { get; set; }
        public string CPF { get; set; }
        public string DataNascimento { get; set; }
        public string Telefone { get; set; }
        public string Email { get; set; }
        public string Endereco { get; set; }
        public string Visita { get; set; }
        public List<Exame> ExamesAgendados { get; set; } = new List<Exame>();
    }

    public class Exame
    {
        public string Nome { get; set; }
        public float Valor { get; set; }
        public int Prazo { get; set; }

        public Exame(string nome, float valor, int prazo)
        {
            Nome = nome;
            Valor = valor;
            Prazo = prazo;
        }
    }
}

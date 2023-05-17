# GUIDb

apriamo visual studio e creiamo un nuovo progetto MAUI

![cattura](https://github.com/leodyrmyshi/GUIDb/assets/116791297/b89df7a3-81f5-44bc-a968-b0c617f5aa94)


dopodichè installiamo la libreria sqlite-net-plc 

![cattura3](https://github.com/leodyrmyshi/GUIDb/assets/116791297/efc35a4d-ae13-4b3c-acdd-2b9ab591202c)


aggiungiamo il file chinook.db e lo mettiamo nella cartella raw

![cattura2](https://github.com/leodyrmyshi/GUIDb/assets/116791297/9bb9b01b-db19-4092-8e3e-2cf5056c4ca7)


una volta fatto tutto ciò, dobbiamo creare una nuova classe. clicchiamo col pulsante destro e scchiacciamo aggiungi e andiamo a selezionare classe e la chiamiamo Recors.cs

![cattura4](https://github.com/leodyrmyshi/GUIDb/assets/116791297/a0561f76-8469-4917-bc5d-296854d21d16)


dentro la classe Rcors.cs dobbiamo scrivere:
###
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;

    namespace dyrmyshi.leo._4H.GUIDb
    {
       public class Album
       {
           public int AlbumId { get; set; }
           public string Title { get; set; }
           public int ArtistId { get; set; }
       }
       
       public class Artist
       {
           public int ArtistId { get; set; }
           public string Name { get; set; }
       }

       public class Track
       {
           public int TrackId { get; set; }
           public string Name { get; set; }
           public int AlbumId { get; set; }
           public int MediaTypeId { get; set; }
           public int GenreId { get; set; }
           public string Composer { get; set; }
           public Int64 Milliseconds { get; set; }
           public Int64 Bytes { get; set; }
           public double UnitPrice { get; set; }

       }
    }
###

mentre in MainPage.xaml dobbiamo scrivere:
###
    <Window x:Class="dyrmyshi.leo._4H.GUIDb.MainWindow"
    <Grid>
        <StackPanel Orientation="Vertical">
            <StackPanel>
                <Button Width="100" Click="Button_Click"></Button>
            </StackPanel>

            <DataGrid x:Name="dgDati"></DataGrid>
        </StackPanel>
    </Grid>
    </Window>
###

nel MainPage.xaml.cs dobbiamo scrivere:
###
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Windows;
    using System.Windows.Controls;
    using System.Windows.Data;
    using System.Windows.Documents;
    using System.Windows.Input;
    using System.Windows.Media;
    using System.Windows.Media.Imaging;
    using System.Windows.Navigation;
    using System.Windows.Shapes;
    using SQLite;

    namespace dyrmyshi.leo._4H.GUIDb
    {
        /// <summary>
        /// Interaction logic for MainWindow.xaml
        /// </summary>
        public partial class MainWindow : Window
        {
            public MainWindow()
            {
                InitializeComponent();
            }

        private void Button_Click(object sender, RoutedEventArgs e)
        {
            var cn1 = new SQLiteConnection("chinook.db");

            List<Artist> tblArtists;

            // Prende tutti gli artisti
            tblArtists = cn1.Query<Artist>("select * from artists where name like 'a%'");
            dgDati.ItemsSource = tblArtists;

        }
      }
    }
###

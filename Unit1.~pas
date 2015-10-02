unit Unit1;

interface

uses
  Windows, Messages, SysUtils, Variants, Classes, Graphics, Controls, Forms,
  Dialogs, StdCtrls, FileCtrl;

type
  TForm1 = class(TForm)
    FileListBox1: TFileListBox;
    DirectoryListBox1: TDirectoryListBox;
    DriveComboBox1: TDriveComboBox;
    FilterComboBox1: TFilterComboBox;
    Edit1: TEdit;
    Edit2: TEdit;
    Button2: TButton;
    Label2: TLabel;
    Button3: TButton;
    Edit3: TEdit;
    Button4: TButton;
    Label3: TLabel;
    Label1: TLabel;
    Button1: TButton;
    procedure Button1Click(Sender: TObject);
    procedure Button2Click(Sender: TObject);
    procedure Button3Click(Sender: TObject);

    procedure Button4Click(Sender: TObject);
    

  private
    { Private declarations }
  public
    { Public declarations }
  end;

var
  Form1: TForm1;



implementation

{$R *.dfm}

procedure TForm1.Button1Click(Sender: TObject);
var dir : string;
var F:TFileStream;

begin
if DirectoryExists(Edit1.Text) then
Label1.Caption:= Edit1.Text + ' Уже создан'

else
begin
dir:=Edit1.Text;
ForceDirectories(dir);
if DirectoryExists(dir) then
Label1.Caption:='Каталог'+dir+'Создан';
end;

end;




procedure TForm1.Button2Click(Sender: TObject);
var F:TFileStream;
begin

F:=TFileStream.Create(Edit2.Text + '.txt',fmOpenWrite OR fmCreate);
Label2.Caption:=(Edit2.Text + '.txt' + ' Создан');


F.Free;
end;


procedure TForm1.Button3Click(Sender: TObject);
var F,A:TFileStream;
begin
F:=TFileStream.Create(Edit2.Text + '.txt',fmOpenRead);
A:=TFileStream.Create('Копия ' + Edit2.Text + '.txt',fmOpenWrite OR fmCreate);
A.CopyFrom(F,F.Size);
F.Free;
A.Free;
end;

function DeleteDir(Dir: String): Boolean;
var
  Found : Integer;
  SearchRec: TSearchRec;
begin
  result := false;
  ChDir(Dir);
  if (IOResult<>0) then
  begin
    ShowMessage('Не могу войти в каталог:' + Dir);
    exit;
  end;
  Found := FindFirst('*.*', faAnyFile, SearchRec);
  while (Found = 0) do
  begin
    if (SearchRec.Name <> '.') and (SearchRec.Name <> '..') then
      if ((SearchRec.Attr and faDirectory) <> 0) then
      begin
        if not DeleteDir(SearchRec.Name) then exit;
      end else
        if not DeleteFile(SearchRec.Name) then
        begin
          ShowMessage('Не могу удалить файл:' + SearchRec.Name);
          exit;
        end;
      Found:=FindNext(SearchRec);
  end;
  FindClose(SearchRec);
  ChDir('..');
  RmDir(Dir);
  result := (IOResult = 0);

end;
  procedure TForm1.Button4Click(Sender: TObject);
  var
dir: string;
begin
dir:=Edit3.Text;
if DeleteDir(Dir)
then Label3.Caption:=(Dir + ' Каталог успешно удален')
else Label3.Caption:=(Dir + ' ошибка при попытки удления');
end;











end.

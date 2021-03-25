     H
      *
     FGameD     CF   E             workstn
      *
     D X               S              2S 0
     D i               S              2S 0
     D Row             S              2S 0
     D Col             S              2S 0
     D Count           S              2S 0
     D Msg             S             70A
     D NumRow          DS                  Qualified Dim(6)
     D  NumCol                        2S 0 Dim(6)
      *
     C
      *
      /Free
          Exsr  SInit;
          Count = 0;
          DoW *In03 = *Off;
            Exsr  SMap;
            Exsr  SValidate;
            Exfmt rec001;
            Exsr  SFind;
            If X > 0;
              Clear Msg;
              Exsr  SMove;
            Else;
              Msg = 'Invalid Value';
            EndIf;
          EndDo;
          *inlr = *On;
      /End-Free
      *
       /Free
         Begsr SValidate;
           If Num001 = 1 and Num002 = 2 and Num003 = 3 and
              Num004 = 4 and Num005 = 5 and Num006 = 6 and
              Num007 = 7 and Num008 = 8 and Num009 = 9 and
              Num010 = 10 and Num011 = 11 and Num012 = 12 and
              Num013 = 13 and Num014 = 14 and Num015 = 15;
               Msg = 'Congratulations you have won in ' +
                      %Char(MUsed) + ' moves';
           EndIf;
          Endsr;
       /End-Free
       /Free
          Begsr SMove;
             If NumRow(Row+1).NumCol(Col) = 0;
                NumRow(Row+1).NumCol(Col) = InpNum;
                NumRow(Row).NumCol(Col)   = 0;
                Count = Count + 1;
             ElseIf NumRow(Row-1).NumCol(Col) = 0;
                NumRow(Row-1).NumCol(Col) = InpNum;
                NumRow(Row).NumCol(Col)   = 0;
                Count = Count + 1;
             ElseIf NumRow(Row).NumCol(Col+1) = 0;
                NumRow(Row).NumCol(Col+1) = InpNum;
                NumRow(Row).NumCol(Col)   = 0;
                Count = Count + 1;
             ElseIf NumRow(Row).NumCol(Col-1) = 0;
                NumRow(Row).NumCol(Col-1) = InpNum;
                NumRow(Row).NumCol(Col)   = 0;
                Count = Count + 1;
             Else;
                Msg = 'Number cannot be moved';
             EndIf;
             MUsed = Count;
          Endsr;
       /End-Free
      *
      /Free
          Begsr SFind;
            For i = 1 to 5;
              X = %Lookup(inpnum:NumRow(i).Numcol);
              If X > 0;
                Row = i;
                Col = X;
                Leave;
              EndIf;
            EndFor;
          Endsr;
      /End-Free
      *
      /Free
         BegSr SMap;
            Num001 = NumRow(2).NumCol(2);
            Num002 = NumRow(2).NumCol(3);
            Num003 = NumRow(2).NumCol(4);
            Num004 = NumRow(2).NumCol(5);
            Num005 = NumRow(3).NumCol(2);
            Num006 = NumRow(3).NumCol(3);
            Num007 = NumRow(3).NumCol(4);
            Num008 = NumRow(3).NumCol(5);
            Num009 = NumRow(4).NumCol(2);
            Num010 = NumRow(4).NumCol(3);
            Num011 = NumRow(4).NumCol(4);
            Num012 = NumRow(4).NumCol(5);
            Num013 = NumRow(5).NumCol(2);
            Num014 = NumRow(5).NumCol(3);
            Num015 = NumRow(5).NumCol(4);
            Num016 = NumRow(5).NumCol(5);
         Endsr;
      /End-Free
      *
      /Free
         Begsr SInit;
            NumRow(1).NumCol(1) = 99;
            NumRow(1).NumCol(2) = 99;
            NumRow(1).NumCol(3) = 99;
            NumRow(1).NumCol(4) = 99;
            NumRow(1).NumCol(5) = 99;
            NumRow(1).NumCol(6) = 99;
            //
            NumRow(2).NumCol(1) = 99;
            NumRow(2).NumCol(2) =  2;
            NumRow(2).NumCol(3) =  5;
            NumRow(2).NumCol(4) =  4;
            NumRow(2).NumCol(5) =  8;
            NumRow(2).NumCol(6) = 99;
            //
            NumRow(3).NumCol(1) = 99;
            NumRow(3).NumCol(2) =  1;
            NumRow(3).NumCol(3) =  6;
            NumRow(3).NumCol(4) =  3;
            NumRow(3).NumCol(5) = 11;
            NumRow(3).NumCol(6) = 99;
            //
            NumRow(4).NumCol(1) = 99;
            NumRow(4).NumCol(2) = 14;
            NumRow(4).NumCol(3) = 10;
            NumRow(4).NumCol(4) = 15;
            NumRow(4).NumCol(5) = 07;
            NumRow(4).NumCol(6) = 99;
            //
            NumRow(5).NumCol(1) = 99;
            NumRow(5).NumCol(2) = 09;
            NumRow(5).NumCol(3) = 13;
            NumRow(5).NumCol(4) = 12;
            NumRow(5).NumCol(5) =  0;
            NumRow(5).NumCol(6) = 99;
            //
            NumRow(6).NumCol(1) = 99;
            NumRow(6).NumCol(2) = 99;
            NumRow(6).NumCol(3) = 99;
            NumRow(6).NumCol(4) = 99;
            NumRow(6).NumCol(5) = 99;
            NumRow(6).NumCol(6) = 99;
            //
         EndSr;
      /End-Free

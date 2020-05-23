# powerdns-pdns-api-vb.net
PowerDns (pdns) Api Vb.net examples

<h2>Usage</h2>

<b>Variables</b>

Dim PowerDnsHostname As String = "127.0.0.1" // power dns server ip address
 
Dim ApiSecret As String = "api secret key"
 
Dim Ns1 As String = "ns1.your-nameserver.net"
 
Dim Ns2 As String = "ns2.your-nameserver.net"
 
Dim Ns3 As String = "ns3.your-nameserver.net"
 
Dim Ns4 As String = "ns4.your-nameserver.net"
 
 
<h2>Read Zones List</h2>
 
    Async Sub ReadALLZones()
        Try
            Liste.Items.Clear()
            Dim client = New PowerDnsClient(uri:=New Uri("http://" + PowerDnsHostname + ":8081/"), apiKey:=ApiSecret)
            Dim zonesEndpoint = client.Servers("localhost").Zones
            Dim zones As List(Of Zone) = Await zonesEndpoint.ReadAllAsync
            For index = 0 To zones.Count - 1
                Liste.Items.Add(zones(index).Name)
            Next
        Catch ex As Exception
            MessageBox.Show(ex.ToString)
        End Try
    End Sub
 
<h2>Create Zone</h2>

    Async Function CreateZone(ZoneName As String) As Task(Of String)
        Try
            Dim client = New PowerDnsClient(uri:=New Uri("http://" + PowerDnsHostname + ":8081/"), apiKey:=ApiSecret)
            Dim zonesEndpoint = client.Servers("localhost").Zones
            Dim zone As New Zone
            zone.Name = ZoneName
            zone.Kind = ZoneKind.Master
            Dim a As New List(Of CanonicalName)
            a.Add(Ns1)
            a.Add(Ns2)
            a.Add(Ns3)
            a.Add(Ns4)
            zone.Nameservers = a
            Await zonesEndpoint.CreateAsync(zone)
            Return "ok"
        Catch ex As Exception
            Return ex.ToString.ToLower
        End Try
    End Function
    
    Private Async Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click
        Dim task As Task(Of String) = CreateZone(ZName.Text)
        Dim result As String = Await task
        MessageBox.Show(result)
    End Sub


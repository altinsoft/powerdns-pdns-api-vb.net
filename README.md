# powerdns-pdns-api-vb.net
PowerDns (pdns) Api Vb.net examples

<h2>Usage</h2>

 Dim PowerDnsHostname As String = "127.0.0.1" // power dns server ip address
 
 Dim ApiSecret As String = "api secret key"
 
 Dim Ns1 As String = "ns1.your-nameserver.net"
 
 Dim Ns2 As String = "ns2.your-nameserver.net"
 
 Dim Ns3 As String = "ns3.your-nameserver.net"
 
 Dim Ns4 As String = "ns4.your-nameserver.net"
 
 
 
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
 
